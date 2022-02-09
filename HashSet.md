  //
    //HashSet添加底层是如何实现的。
    //HashSet的底层是HashMap
    //2.添加一个元素时，先得到Hash值转换成索引值
    //3.找到存储数据表table，看这个索引位置是否存放有元素
    //4.如果没有，直接加入
    //5.如果有，调用equals比较，如果相同，就放弃添加，如果不相同，则添加到最后。
    //6.在Java8中，如果一条链表的元素个数超过TREEIFY_THRESHOLD默认是8，并且talbe的大小>=MIN_TREEIFY_CAPACITY(默认值是64)
    //就会进行树化(在JDK8中如果一条链表的元素超过了默认值)

//key对应的hash值
static final int hash(Object key) {
        int h;
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
//要讲清楚HashSet,本质上是HashMap
final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
        Node<K,V>[] tab; Node<K,V> p; int n, i;
        //如果为空则进行扩容为16个空间
        if ((tab = table) == null || (n = tab.length) == 0)
            n = (tab = resize()).length;

        //(1)根据key，得到hash去计算key应该存放到table表的哪个索引位置
        //并把这个位置对象，赋给P
        //(2)判断 p是否为 null
        //(2.1)如果p为null则表示还没有存放元素，就创建一个Node(key="java, value = PRESIDENT)
        //(2.2)就放在tab[i]
        //threshold
        if ((p = tab[i = (n - 1) & hash]) == null)
            tab[i] = newNode(hash, key, value, null);
        else {
            //需要的局部变量表示方法
            Node<K,V> e; K k;
            if (p.hash == hash &&
            //如果当前索引位置对应的链表的第一个元素和准备添加的key的hash值一样
            //并且满足下列两个条件之一：
            //(1)准备加入的key和p指向的Node结点的key是同一个对象
            //(2)p指向的Node结点的key的equals()和准备加入的key经过比较后相///同

                ((k = p.key) == key || (key != null && key.equals(k))))
                e = p;
            //在判断是不是一棵红黑树，如果是一颗红黑树，就进行添加
            else if (p instanceof TreeNode)
                e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
            else {//如果table对应索引位置。已经是一个链表，就使用or循环比较
            //(1)依次和该链表的每一个元素比较后都不相同，则加入到该链表的最//后
            //(2)依次比较的过程中，如果有相同的情况下break
            //
                for (int binCount = 0; ; ++binCount) {
                    if ((e = p.next) == null) {
                        p.next = newNode(hash, key, value, null);
                        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                            treeifyBin(tab, hash);
                        break;
                    }
                    if (e.hash == hash &&
                        ((k = e.key) == key || (key != null && key.equals(k))))
                        break;
                    p = e;
                }
            }
            if (e != null) { // existing mapping for key
                V oldValue = e.value;
                if (!onlyIfAbsent || oldValue == null)
                    e.value = value;
                afterNodeAccess(e);
                return oldValue;
            }
        }
        ++modCount;
        if (++size > threshold)
            resize();
        afterNodeInsertion(evict);
        return null;
    }
    //1.HashSet底层是HashMap,第一次添加时，table数组扩容到16，临界值(threehold)是16*加载因子。
    //如果table数组使用到了临界值12，就会扩容到16*2=32，新的临界值就是32*0.75=24，依次类推
    3.在Java8中，如果一条链表的元素分数到达TREEIFY_THRESHOLD并且table大小为>=MIN_TREEIFY_CAPACITY(默认64)，就会进行树化，否则仍然采用数组扩容机制。