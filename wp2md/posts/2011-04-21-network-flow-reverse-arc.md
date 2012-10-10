---
layout: post
title: 网络流中反向弧的作用
category : acmicpc
tags : [acmicpc]
---

<strong>一切始于我不理解反向弧的作用。</strong>    
    
求解最大流问题，可以使用寻找增广路的做法求解。增广路的什么资料的太多了，请自行Google，不然会看不懂的。    
找到一条增广路的时候，我们不仅要把残余网络中正向弧c[u,v]的流量减少，还要相应的减少其反向弧c[v,u]的流量？这是为什么呢？    
来个例子吧！    
<pre>一个图,(请自行画图),描述(u -&gt; v, 流量)，6个顶点，1为源点，6为汇点。    
1 -&gt; 2  2    
1 -&gt; 3  2    
2 -&gt; 4  2    
3 -&gt; 4  2    
2 -&gt; 5  2    
5 -&gt; 6  3    
4 -&gt; 6  2</pre>    
先假设我们更新残余网络的时候只减少正向弧的流量，不增加反向弧的流量。    
假设此时找到一条增广路：1 -&gt; 2 -&gt; 4 -&gt; 6 , 增广路上的流量为2。    
现在又开始找另一条，假如找到了 1 -&gt; 3 -&gt; 4，但是此时你应该发现没有路了！但是实际上图中的最大流并不是2，正确的是4！    
所以最好的做法是 1 -&gt; 2 -&gt; 5 -&gt; 6 一条路，1 -&gt; 3 -&gt; 4 -&gt; 6 一条路，最大流为4。为什么会这样呢？    
因为我们没有选好一条增广路(假如不增加反向弧的流量)。    
    
现在我们根据增广路更新残余网络的时候不仅减少正向弧的流量，还增加反向弧的流量。    
即 正向弧(u,v): c[u][v] -= minflow; c[v][u] += minflow;    
那么当我们找到第一条增广路：1 -&gt; 2 -&gt; 4 -&gt; 6 , 增广路上的流量为2的时候，    
更新残余网络，(新的残余网络请自行绘图，不要老是依赖别人，O(∩_∩)O~)。    
当找 1 -&gt; 3 -&gt; 4 的时候，就可以跑向2 -&gt; 5 -&gt; 6 了，那么第二条增广路路就是：1 -&gt; 3 -&gt; 4 -&gt; 2 -&gt; 5 -&gt; 6 ，流量为2，看出来了吧，这就是作用！    
    
我建议再把按照第二条增广路更新的残余网络画出来，因为这跟找 1 -&gt; 2 -&gt; 5 -&gt; 6 ，1 -&gt; 3 -&gt; 4 -&gt; 6 之后的结果一样的。    
    
其实就是第一条路和第二条路可以互相交换部分路径，然而可交换路径的流最多就是2和4之间的能传送的流。交换增广路径的流！正向弧(u,v): c[u][v] -= minflow; c[v][u] += minflow; 的目的就是为了能让各个增广路能交换流，保证总能找到合适流量路线。    
要是不理解，不要怪我啊，大家背吧，没事的！    
    
以上是我这名菜鸟的见解，要是出错了请提出来。还有就是如果误导了大家可千万不要怪我啊！不是我的错！    
    
在此要感谢QQ昵称为冰雪城的学长的讲解，他的信息我就不再透露了，没经过他同意啊，呵呵。