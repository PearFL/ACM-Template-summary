# ACM代码整合

[TOC]

如果发现文章中有不正确的地方，欢迎联系本人，感谢指出问题的每个人

PS：本文一切代码均有C/C++编写，参与JAVA组的人可以理解思想了以后尝试改写



### ！！！特别提醒

1、注意程序最后应有返回值，且返回值为0

2、万能头文件可以使用(bits/stdc++.h)，比赛中使用c++的方法是，记得开全局空间using namespace std;

3、熟悉STL用法，包括vector、set、map、pair等结构的用法，这会给你剩下许多时间

4、例如max_element、lower_bound函数的用法请熟悉

5、在不能保证自己的算法的绝对正确性的情况下，可以选择保住现有的分，而不去尝试难度较高且自己没有把握的方法



### 1、最大公约数gcd

```c++
int gcd(int a,int b){
	return b == 0 ? a : gcd(b,a%b);
} 
```



### 2、最小公倍数lcm

```c++
int gcd(int a,int b){
	return b == 0 ? a : gcd(b,a%b);
} 

int lcm(int a,int b){
	return a*b/gcd(a,b);
}
```



### 3、Fibonacci数列 

采用记忆化搜索的写法，或者使用状态转移的方法推导

- 记忆化搜索写法

```c++
int dp[1005];
int dfs(int n){
	if(n==1 || n==2){
		return 1;
	}
	if(dp[n] > 0){
		return dp[n];
	}else{
		dp[n] = dfs(n-1) + dfs(n-2);
		return dp[n];
	}	
}

```


- 状态转移写法

```c++
int dp[1000];
dp[1] = 1;
dp[2] = 1;
for(int i=3;i<1000;i++){
  dp[i] = dp[i-1] + dp[i-2];
} 
```



### 4、memset初始化

- memset在整形数组中推荐两种用法

```c++
int dp[1005];
memset(dp,0,sizeof(dp));//dp中的值全部置为了0
memset(dp,-1,sizeof(dp));//dp中的值全部置为了-1
```

 有人问1,2,3其他的可行，当然是不行的，至于原因有兴趣想要知道的话，可以在网上了解

- memset在char数组中
```c++
char str[1005];
memset(str,0,sizeof(str));
```
这样就是将char数组重置了，在多组输入的情况中，memset将会是一个非常高效的方法



### 5、fill初始化

```c++
int dp[100];
fill(dp,dp+10,5);
```

此时dp[0] -> dp[9]的值全部被置为了5

```c++
char str[100];
fill(str,str+10,'m');
```

此时str[0] -> str[9]的值全部被置为了m



以上两个例子相信大家一下子就对fill有所了解了吧，在实际运用中大家可以根据自己的需要使用fill和memset



### 6、ctype.h头文件

|   函数名称   |         函数原型         |                  函数功能                   |            函数返回            |
| :------: | :------------------: | :-------------------------------------: | :------------------------: |
| isalpha  | int isalpha(char ch) |                检查ch是否是字母                | 是字母返回非0（在vs2015中为2），否则返回 0 |
| iscntrl  | int iscntrl(int ch)  |  检查ch是否控制字符(其ASCII码在0和0x1F之间,数值为 0-31)  |        是返回非0,否则返回 0        |
| isdigit  | int isdigit(char ch) |             检查ch是否是数字(0-9)              |        是返回非0,否则返回0         |
| isgraph  | int isgraph(int ch)  | 检查ch是否可显示字符(其ASCII码在0x21到0x7E之间),不包括空格  |        是返回非0,否则返回0         |
| islower  | int islower(int ch)  |             检查ch是否小写字母(a-z)             |        是返回非0,否则返回0         |
| isupper  | int isupper(int ch)  |            检查ch是否是大写字母(A-Z)             |        是返回非0,否则返回0         |
| tolower  | int tolower(int ch)  |              将ch字符转换为小写字母               |      返回ch所代表的字符的小写字母       |
| toupper  | int toupper(int ch)  |              将ch字符转换成大写字母               |         与ch相应的大写字母         |
| isalnum  | int isalnum(int ch)  |              检查ch是否是字母或数字               |      是字母或数字返回非0,否则返回0      |
| isprint  | int isprint(int ch)  | 检查ch是否是可打印字符(包括空格),其ASCII码在0x20到0x7E之间  |        是返回非0,否则返回0         |
| ispunct  | int ispunct(int ch)  | 检查ch是否是标点字符(不包括空格),即除字母,数字和空格以外的所有可打印字符 |        是返回非0,否则返回0         |
| isspace  | int isspace(int ch)  |        检查ch是否是空格符和跳格符(控制字符)或换行符         |        是返回非0,否则返回0         |
| isxdigit | int isxdigit(int ch) |    检查ch是否是一个16进制数学字符(即0-9,或A-F,或a-f)    |        是返回非0,否则返回0         |
| isascii  | int isascii(int ch)  |           测试参数是否是ASCII码0-127            |        是返回非0,否则返回0         |



### 7、素数系列

- 埃拉托斯特尼筛法，或者叫埃氏筛法

```c++
const int N = 100005;  
bool prime[N];  
void init(){  
    for(int i=2;i<N;i++) prime[i]=true;//先全部初始化为素数  
    for(int i=2;i*i<N;i++){  
        if(prime[i]){//如果i是质数  
            for(int j=i*i;j<N;j+=i){//从i的两倍开始的所有的倍数(i*i也行)  
                prime[j] = false;  
            }  
        }  
    }  
}  
```

- 预处理每个数的所有质因数
```c++
const int N = 100000 + 5;  
vector<int > prime_factor[N];  
void init(){  
    for(int i = 2; i < N; i ++){  
        if(prime_factor[i].size() == 0){//如果i是质数   
            for(int j = i; j < N; j += i){  
                prime_factor[j].push_back(i);   
            }  
        }  
    }  
} 
```

- 比如预处理每个数的所有因数

```c++
const int N = 100000 + 5;  
vector<int > factor[N];  
void init(){  
    for(int i = 2; i < N; i ++){  
        for(int j = i; j < N; j += i){  
            factor[j].push_back(i);  
        }  
    }  
}
```

- 预处理每个数的质因数分解

```c++
const int N = 100000 + 5;  
vector<int > prime_factor[N];  
void init(){  
    int temp;  
    for(int i = 2; i < N; i ++){  
        if(prime_factor[i].size() == 0){  
            for(int j = i; j < N; j += i){  
                temp = j;  
                while(temp % i == 0){  
                    prime_factor[j].push_back(i);  
                    temp /= i;  
                }  
            }  
        }  
    }  
}
```

http://blog.csdn.net/laichilizi/article/details/79390020

质因数分解题目↑（输入两个整数a、b，每行输出一个数的分解，形如k=a1*a2*a3...(a1<=a2<=a3....）

```c++
#include<bits/stdc++.h>    
using namespace std;    
const int N = 100000 + 5;    
vector<int > prime_factor[N];    
void init(){    
    int temp;    
    for(int i = 2; i < N; i ++){    
        if(prime_factor[i].size() == 0){    
            for(int j = i; j < N; j += i){    
                temp = j;    
                while(temp % i == 0){    
                    prime_factor[j].push_back(i);    
                    temp /= i;    
                }    
            }    
        }    
    }    
}    
int main()  
{    
    init();   
      
    int a,b;  
    scanf("%d %d",&a,&b);  
    vector<int>::iterator it;  
    for(int i=a;i<=b;i++){  
        cout<<i<<"=";  
        for(it = prime_factor[i].begin(); it != prime_factor[i].end(); it++){  
            if(it != prime_factor[i].end()-1) cout << *it <<"*";  
            else cout<<*it<<endl;  
        }  
              
    }   
}  
```



### 8、BFS系列

http://blog.csdn.net/laichilizi/article/details/75024841

- 马的移动↑，BFS入门题

http://blog.csdn.net/laichilizi/article/details/79383954

- 学霸的迷宫↑，BFS+记录操作方向

```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

const int INF = 100000000;
//使用pair表示状态时，使用typedef会更方便一些 
typedef pair<int,int> P;
char maze[MAX_N][MAX_M + 1];
int N,M;
int sx,sy; //起点坐标 
int gx,gy; //终点坐标

int d[MAX_N][MAX_M]; //到各个位置的最短距离的数组 
//4个方向移动的向量 
int dx[4] = {1,0,-1,0},dy[4] = {0,1,0,-1}; 

// 求从(sx,sy)到(gx,gy)的最短距离
// 如果无法到达，则是INF

int bfs(){
	queue<P> que;
	//把所有的位置都初始化为INF
	for(int i=0;i<N;i++)
		for(int j=0;j<M;j++) d[i][j] = INF;
	//将起点加入队列，并把这一地点的距离设置为0
	que.push(P(sx,sy));
	d[sx][sy] = 0; 
	
	//不断循环直到队列的长度为0 
	while(que.size()){
		//从队列的最前端取出元素
		P p = que.front();que.pop();
		//如果取出的状态已经是终点，则结束搜索
		if(p.first == gx && p.second == gy) break;
		
		//四个方向的循环
		for(int i=0;i<4;i++){
			//移动之后的位置记为(nx,ny)
			int nx = p.first + dx[i],ny = p.second + dy[i];
			
			//判断是否可以移动以及是否已经访问过 (d[nx][ny]!=INF即为已经访问过)
			if(0 <= nx && nx<N && 0<=ny && ny<M && maze[nx][ny] != '#' && d[nx][ny] = INF){
				//可以移动的话，则加入到队列，并且到该位置的距离确定为到p的距离+1
				que.push(P(nx,ny));
				d[nx][ny] = d[p.first][p.second] + 1; 
			}
		} 
	}
	return d[gx][gy];
	 
} 

void solve(){
	int res = bfs();
	printf("%d\n",res);
}

int main(){
	
	return 0;
}
```

### 9、DFS系列

http://blog.csdn.net/laichilizi/article/details/79388913

- 正则问题↑，一个由x()|组成的正则表达式。输入长度不超过100，保证合法，求这个正则表达式能接受的最长字符串的长度

http://blog.csdn.net/laichilizi/article/details/78714582

- POJ-2386，简单区域连通问题，↑

```c++
//POJ-2386
/*
10 12
W........WW.
.WWW.....WWW
....WW...WW.
.........WW.
.........W..
..W......W..
.W.W.....WW.
W.W.W.....W.
.W.W......W.
..W.......W.
*/
/*
3
*/

#include<cstdio>  
#include<cstring>  
#include<algorithm>  
using namespace std;  
typedef long long ll;  
  
int n,m;  
char field[105][105]; //园子  
  
void dfs(int x,int y){  
    field[x][y]='.';  
    for(int dx = -1;dx <= 1;dx++){  
        for(int dy = -1;dy <= 1;dy++){  
            int nx=x+dx,ny=y+dy;  
            if(nx>=0 && nx<n && ny<m && ny>=0 && field[nx][ny] =='W') dfs(nx,ny);  
        }  
    }  
    return ;  
}  
  
void solve(){  
    int res = 0;  
    for(int i=0;i<n;i++){  
        for(int j=0;j<m;j++){  
            if(field[i][j]=='W'){  
                dfs(i,j);  
                res++;  
            }  
        }  
    }  
    printf("%d\n",res);  
}  
  
void init(){  
    scanf("%d %d",&n,&m);  
    for(int i=0;i<n;i++)  
        scanf("%s",field[i]);  
}  
  
int main()  
{  
    //freopen("input.txt","r",stdin);  
    init();  
    solve();  
  
  
    return 0;  
}
```



### 10、动态规划（01背包，完全背包）

- 01背包（记忆化搜索）

```c++
#include<bits/stdc++.h>  
using namespace std;  
typedef long long ll;  
  
int n,W;  
int dp[105][10005];  
int w[105],v[105];  
  
int rec(int i,int j){  
    if(dp[i][j] >= 0){  
        return dp[i][j];  
    }  
    int res;  
    if(i == n){  
        res = 0;  
    }else if(j < w[i]){  
        res = rec(i + 1,j);  
    }else{  
        res = max(rec(i + 1,j),rec(i + 1,j - w[i])+v[i]);  
    }  
      
    return dp[i][j] = res;  
}  
  
int main()  
{  
    scanf("%d %d",&n,&W);  
      
    for(int i=0;i<n;i++){  
        scanf("%d %d",&w[i],&v[i]);   
    }  
      
    memset(dp,-1,sizeof(dp));  
      
    cout<<rec(0,W)<<endl;  
      
      
    return 0;  
}  
```

- 01背包（二维DP）
```c++
#include<bits/stdc++.h>  
using namespace std;  
typedef long long ll;  
  
int n,W;  
int dp[105][10005];  
int w[105],v[105];  
  
int main()  
{  
    scanf("%d %d",&n,&W);  
      
    for(int i=0;i<n;i++){  
        scanf("%d %d",&w[i],&v[i]);   
    }  
      
    memset(dp,0,sizeof(dp));  
      
    for(int i=n-1;i>=0;i--){  
        for(int j=0;j<=W;j++){  
            if(j < w[i]){  
                dp[i][j] = dp[i + 1][j];  
            }else{  
                dp[i][j] = max(dp[i+1][j],dp[i+1][j-w[i]]+v[i]);  
            }  
        }  
    }  
      
    cout<<dp[0][W]<<endl;  
      
    return 0;  
}  
```

- 01背包（一维最简化）

```c++
int dp[MAX_W +1];

void solve(){
    for(int i=0;i<n;i++){
        for(int j=W;j>=w[i];j--){
            dp[j] = max(dp[j],dp[j-w[i]]+v[i]);
        }
    }
    printf("%d\n",dp[W]);
}
```

- 完全背包（一维最简化）

```c++
int dp[MAX_W +1];

void solve(){
    for(int i=0;i<n;i++){
        for(int j=w[i];j<=W;j--){
            dp[j] = max(dp[j],dp[j-w[i]]+v[i]);
        }
    }
    printf("%d\n",dp[W]);
}
```
- 多重背包（一维最简化）
```c++
#include <iostream>  
#include <stdio.h>  
#include <string.h>  
#include <algorithm>  
using namespace std;  
  
int main()  
{  
    int T,n,m;  
    int v[105],w[105],num[105],dp[105];  
    cin>>T;  
    while(T--)  
    {  
        cin>>m>>n;  
        for(int i=0;i<n;i++)  
            cin>>v[i]>>w[i]>>num[i];  
        memset(dp,0,sizeof(dp));  
        for(int i=0;i<n;i++)  
            for(int j=0;j<num[i];j++)  
                for(int k=m;k>=v[i];k--)  
                    dp[k]=max(dp[k],dp[k-v[i]]+w[i]);  
        cout<<dp[m]<<endl;  
    }  
    return 0;  
} 
```


### 11、并查集

```c++
int par[MAX_N];
int rank[MAX_N];

//初始化n个元素 
void init(int n){
	for(int i=0;i<n;i++){
		par[i] = i;
		rank[i] = 0;
	}
}

//查询树的根 
int find(int x){
	if(par[x] == x){
		return x;
	}else{
		return par[x] = find(par[x]);
	}
}

//合并x和y所属的集合 
void unite(int x,int y){
	x = find(x);
	y = find(y);
	if(x == y) return;
	if(rank[x] < rank[y]){
		par[x] = y;
	}else{
		par[y] = x;
		if(rank[x] == rank[y]) rank[x]++;
	}
}

//判断x和y是否属于同一个集合
bool same(int x,int y){
	return find(x) == find(y);
}
```

经典例题：hdu1232

```c++
#include<cstdio>
using namespace std;

int par[1005];
int rank[1005];

//初始化n个元素
void init(int n){
	for(int i=1;i<=n;i++){
		par[i] = i;
		rank[i] = 0;
	}
}

//查询树的根
int find(int x){
	if(par[x] == x){
		return x;
	}else{
		return par[x] = find(par[x]);
	}
}

//合并x和y所属的集合
void unite(int x,int y){
	x = find(x);
	y = find(y);
	if(x == y) return;
	if(rank[x] < rank[y]){
		par[x] = y;
	}else{
		par[y] = x;
		if(rank[x] == rank[y]) rank[x]++;
	}
}

//判断x和y是否属于同一个集合
bool same(int x,int y){
	return find(x) == find(y);
}

int main()
{
    int n,m;
    while(~scanf("%d%d",&n,&m)){
        if(n == 0) break;
        init(n);
        for(int i=0;i<m;i++){
            int x,y;
            scanf("%d%d",&x,&y);
            unite(x,y);
        }
        int ans = 0;
        for(int i=1;i<=n;i++){
            if(par[i] == i) ans ++;
        }
        printf("%d\n",ans-1);
    }

    return 0;
}

```



### 12、树状数组

```c++
int lowbit(int x){  
    return x&(-x);  
}  

void add(int x,int y){  
    while(x<=n){  
        c[x]+=y;  
        x+=lowbit(x);  
    }  
}  

//用于求序列中小于等于数字x的元素的个数
int sum(int x){  
    int ans=0;  
    while(x>0){  
        ans+=c[x];  
        x-=lowbit(x);  
    }       
    return ans;  
} 
```

http://blog.csdn.net/laichilizi/article/details/79450529

- 求逆序数↑

```c++
#include<iostream>  
#include<cstdio>  
using namespace std;  
int n;  
int aa[100005];  
int c[100005];  
int a[100005];  
int lowbit(int x)  
{  
    return x&(-x);  
}  
void add(int x,int y)  
{  
    while(x<=n)  
    {  
        c[x]+=y;  
        x+=lowbit(x);  
    }  
}  
int sum(int x)  
{  
    int ans=0;  
    while(x>0)  
    {  
        ans+=c[x];  
        x-=lowbit(x);  
    }  
       
    return ans;  
}  
   
int main()  
{  
    scanf("%d",&n);  
    for(int i=0;i<n;i++)  
    {  
        scanf("%d",&a[i]);  
    //  aa[a[i]]=a[i];  
    }   long long aans=0;  
    for(int i = 0 ; i<n;i++)  
    {  
        add(a[i],1);  
        aans+=i-sum(a[i]-1);  
    //  cout << i;  
    //  cout << sum(a[i]-1)<<endl;;  
    }  
   
    printf("%lld\n",aans);  
    return 0;  
} 
```



### 13、快速幂 and 矩阵快速幂

- 快速幂

```c++
typedef long long ll;
ll ksm(ll x,ll n,ll mod){
	ll res = 1;
	x = x % mod;
	while(x > 0){
		if(n & 1) res = res * x % mod;
		x = x * x % mod;
		n >>= 1;
	}
	return res;
}
```

- 矩阵快速幂

http://blog.csdn.net/wust_zzwh/article/details/52058209

```c++
#include<bits/stdc++.h>  
using namespace std;  
typedef long long ll;  
const int MOD=10000;  
struct mat  
{  
    ll a[2][2];  
};  
mat mat_mul(mat x,mat y)  
{  
    mat res;  
    memset(res.a,0,sizeof(res.a));  
    for(int i=0;i<2;i++)  
        for(int j=0;j<2;j++)  
        for(int k=0;k<2;k++)  
        res.a[i][j]=(res.a[i][j]+x.a[i][k]*y.a[k][j])%MOD;  
    return res;  
}  
void mat_pow(int n)  
{  
    mat c,res;  
    c.a[0][0]=c.a[0][1]=c.a[1][0]=1;  
    c.a[1][1]=0;  
    memset(res.a,0,sizeof(res.a));  
    for(int i=0;i<2;i++) res.a[i][i]=1;  
    while(n)  
    {  
        if(n&1) res=mat_mul(res,c);  
        c=mat_mul(c,c);  
        n=n>>1;  
    }  
    printf("%I64d\n",res.a[0][1]);  
}  
int main()  
{  
    int n;  
    while(~scanf("%d",&n)&&n!=-1)  
    {  
        mat_pow(n);  
    }  
    return 0;  
}
```

### 14、最短路

http://blog.csdn.net/acm_1361677193/article/details/48211319



### 15、string

http://blog.csdn.net/tengfei461807914/article/details/52203202



### 16、二分搜索

二分模型

```c++
while(l < r-1){
        int mid = r + (l - r)>> 1;
        if() l = mid;
        else r = mid;
    }
```



http://blog.csdn.net/laichilizi/article/details/79388555

- 分巧克力↑，经典二分题



### 17、字符串函数

- 字符处理函数：ctype.h

```
int isdigit(int ch)  ;//是否为数字，即ch是否是0-9中的字符
int isxdigit(int ch) ;//是否为十六进制数字，即ch是否是0-9  a-z A-Z 中的字符
int isalpha(int ch)  ;//是否为字母
int isalnum(int ch)  ;//是否为字母或数字
int islower(int ch)  ;//是否为小写字母
int isupper(int ch)  ;//是否为大写字母
int tolower(int ch)  ;//转换为小写字母
int toupper(int ch)  ;//转换为大写字母
```

- 字符串转换函数：stdlib.h

**字符转换为数字：**

```
double atof(char  *str) ; //将字符串str转换为double型数字
int    atoi (char  *str) ; //将字符串str转换为int 型数字
long   atol(char  *str) ; //将字符串str转换为long int 型数字
```

**数字转换为字符：**

```
//将int型数字digit按radix进制转换成字符串destStr
char * itoa (int digit, char *destStr, int radix) ;
//同理将long型数字转换成字符串
char * ltoa (long digit, char *destStr, int radix) ;
//同理将unsignedlong型数字转换成字符串
char * ultoa (long digit, char *destStr,int radix) ;
```

【以上库函数能够用于进制的转换】

类似函数还有：

```
double strtod(char *, char **) ;
long strtol(char *, char **, int) ;
unsigned long strtoul(char *, char **, int) ;
```

- 字符串操作函数：string.h

```
char * strcpy (char *s1, char *s2) ; //将字符串s2拷贝到数组s1中。
char * strncpy(char *s1,char *s2) ; //将字符串s2的最多n个字符拷贝到数组s1中
char * strcat (char *s1, char * s2) ; //将字符串s2连接在字符串s1尾部
char * strncat(char *s1, char *s2, size_tn) ; //将字符串s2中最多n个字符连接在s1之后
```

【注意：以上操作都要求目标字符数组有足够的存储空间】

 

- 符串比較函数：string.h

```
//比較字符串s1，s2.假设s1等于小于或大于s2。分别返回0。负值,正值
int strcmp(char *s1, char *s2 ) ;
int stricmp(char *s1, char *s2) ;//不区分大写和小写地比較两字符串
int strncmp(char *s1, char *s2, size_t n)  ;//比較两字符串的至多n个字符
```

- 字符串查找函数：string.h

```
//在字符串str中查找字符ch第一次出现的位置，假设找到了，就返回str中ch的指针，否则返回NULL
char *strchr(char*str, int ch) ;
//查找字符串str中字符ch的最后一次出现的位置(即：从后往前查找)
char*strrchr(char *str, int ch) ;
//查找字符串str1中第一次出现字符串str2的位置
char *strstr(char*str1, char *str2) ;
//查找字符串str2中随意字符在字符串str1中首次出现的位置。
char*strpbrk(char *str1, char *str2)
```

其他函数：

```
char *strrev(char * ) ; //字符串逆序函数
size_t strlen(char * str) ;//測字符串str的长度
```

注意：

strncpy( ) , strncat( ) , strncmp( ) ,这些函数仅仅能对两个不同的字符串操作，不能对同一字符串的不同部分操作。假设须要这么做，能够使用内存函数。

若把目标字符串初始置空，strncat()能够完毕非常多功能的操作。能够替代strncpy( )的功能，还能够提取子串等。

 

### 18、set & multiset



### 19、map & multimap



### 20、queue & priority_queue

- queue

queue入队，如例：q.push(x); 将x 接到队列的末端。

queue出队，如例：q.pop(); 弹出队列的第一个元素，注意，并不会返回被弹出元素的值。

访问queue队首元素，如例：q.front()，即最早被压入队列的元素。

访问queue队尾元素，如例：q.back()，即最后被压入队列的元素。

判断queue队列空，如例：q.empty()，当队列空时，返回true。

访问队列中的元素个数，如例：q.size()



- priority_queue

empty()  如果优先队列为空，则返回真 

pop()  删除第一个元素 

push()  加入一个元素 

size()  返回优先队列中拥有的元素的个数 

top()  返回优先队列中有最高优先级的元素 



### 21、stack

empty() 堆栈为空则返回真

pop() 移除栈顶元素

push() 在栈顶增加元素

size() 返回栈中元素数目

top() 返回栈顶元素



### 22、vector

http://blog.csdn.net/duan19920101/article/details/50617190/



### 23、贪心算法

http://blog.csdn.net/qq_32400847/article/details/51336300



### 24、数制转换

http://blog.csdn.net/laichilizi/article/details/79381732
 


### 25、LCS

只计算LCS的数目
```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

char a[1005],b[1005],ans[1005];
int dp[1005][1005];
int main()
{
	//freopen("input.txt","r",stdin);

	scanf("%s %s",a+1,b+1);
	int n = strlen(a+1);
	int m = strlen(b+1);
	memset(dp,0,sizeof(dp));

	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(a[i] == b[j]){
				dp[i][j] = dp[i-1][j-1] + 1;
			}else{
				dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
			}
		}
	}

	cout<<dp[n][m]<<endl;

	return 0;
}
```

除了LCS的数目，还输出对应的子串
```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

char a[1005],b[1005],ans[1005];
int dp[1005][1005];
int main()
{
	//freopen("input.txt","r",stdin);

	scanf("%s %s",a+1,b+1);
	int n = strlen(a+1);
	int m = strlen(b+1);
	memset(dp,0,sizeof(dp));

	for(int i=1;i<=n;i++){
		for(int j=1;j<=m;j++){
			if(a[i] == b[j]){
				dp[i][j] = dp[i-1][j-1] + 1;
			}else{
				dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
			}
		}
	}
	int cur = 0;
	for(int i=n,j=m;dp[i][j];--i,--j){
		while(dp[i][j] == dp[i-1][j]) --i;
		while(dp[i][j] == dp[i][j-1]) --j;
		ans[cur++] = a[i];
	}

	reverse(ans,ans+cur);
	//ans[cur] = '\0';
	printf("%s\n",ans);

	return 0;
}
```

### 26、LIS
```c++
#include<bits/stdc++.h>  
using namespace std;  
#define INF 0x3f3f3f3f  
typedef long long ll;  
  
int dp[105];  
int a[105];  
  
int main()  
{  
    int n;  
    scanf("%d",&n);  
    for(int i=0;i<n;i++) scanf("%d",&a[i]);  
      
    int res = 0;  
    for(int i=0;i<n;i++){  
        dp[i] = 1;  
        for(int j=0;j<i;j++){  
            if(a[j] < a[i]){ //如果是包括相等，就改为<=   
                dp[i] = max(dp[i],dp[j]+1);  
            }  
        }  
        res = max(res,dp[i]);   
    }  
    cout<<res<<endl;  
  
    return 0;  
}
```

### 27、最大字段和
```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

ll dp[50005];

ll solve(int n,ll *dp){
	ll ans = 0,b = 0;
	for(int i=0;i<n;i++){
		if(b>=0) b+=dp[i];
		else b = dp[i];
		if(b>ans) ans = b;
	}
	return ans;
}

int main(){
	//freopen("input.txt","r",stdin);
	int n;
	scanf("%d",&n);
	memset(dp,0,sizeof(dp));

	for(int i=0;i<n;i++) scanf("%lld",&dp[i]);
	ll p = solve(n,dp);
	cout<<p<<endl;

	return 0;
}
```

### 28、循环数组最大字段和
```c++
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;

ll dp[50005];

ll solve(int n,ll *dp){
	ll ans = 0,b = 0;
	for(int i=0;i<n;i++){
		if(b>=0) b+=dp[i];
		else b = dp[i];
		if(b>ans) ans = b;
	}
	return ans;
}

int main(){
	freopen("input.txt","r",stdin);
	int n,sum = 0;
	scanf("%d",&n);
	memset(dp,0,sizeof(dp));

	for(int i=0;i<n;i++){
		scanf("%lld",&dp[i]);
		sum += dp[i];
	}
	ll ans1 = solve(n,dp);

	for(int i=0;i<n;i++) dp[i] = -dp[i];
	ll ans2 = solve(n,dp);
	ll ans = max(ans1,sum+ans2);

	cout<<ans<<endl;

	return 0;
}
```

### 29、最小正字段和
```c++
#include<iostream>  
#include<cstdio>  
#include<cstring>  
#include<algorithm>  
using namespace std;  
typedef long long LL;  
#define INF 0x3f3f3f3f;

struct node{  
    LL a;  
    int id_mi;  
    int id_ma;  
};  
bool operator <(node a,node b){  
    return a.a<b.a;  
}  
node dp[50010];  
int main(){  
    int n,a,i,j;  
    scanf("%d",&n);  
    LL ans=0;  
    dp[0].a=0;  
    dp[0].id_mi=0;  
    dp[0].id_ma=0;  
    for(i=1;i<=n;i++){  
        scanf("%lld",&dp[i].a);  
        dp[i].a+=dp[i-1].a;  
        dp[i].id_mi=i;  
        dp[i].id_ma=i;  
          
    }  
    sort(dp,dp+1+n);  
    j=0;  
    for(i=1;i<=n;i++)  
    {  
        if(dp[i].a==dp[j].a){  
            dp[j].id_mi=max(dp[j].id_mi,dp[i].id_mi);  
            dp[j].id_ma=min(dp[j].id_ma,dp[i].id_ma);  
        }  
        else dp[++j]=dp[i];  
    }  
    for(i=0;i<j;i++){  
        if(dp[i].id_mi<dp[i+1].id_ma&&dp[i+1].a-dp[i].a>0&&(ans==0||ans>dp[i+1].a-dp[i].a)){  
            ans=dp[i+1].a-dp[i].a;  
        }  
    }  
    cout<<ans<<endl;  
    return 0;  
}  
```

### 30、大数运算
http://blog.csdn.net/tt2767/article/details/45420067

### 31、Trie
```c++
const int MAX_N = 10000;  // Trie 树上的最大结点数
const int MAX_C = 26;  // 每个结点的子结点个数上限
struct Trie {
    int *ch[MAX_N];  // ch 保存了每个结点的 26 个可能的子结点编号，26 对应着 26 种小写字母，也就是说，插入的字符串全部由小写字母组成。初始全部为 -1
    int tot;  // 总结点个数（不含根结点），初始为 0
    int cnt[MAX_N];  // 以当前结点为终端结点的 Trie 树中的字符串个数

    void init() {  // 初始化 Trie 树，根结点编号始终为 0
        tot = 0;
        memset(cnt, 0, sizeof(cnt));
        memset(ch, 0, sizeof(ch));  // 将 ch 中的元素初始化为 NULL
    }

    void insert(char *str) {
        int p = 0;  // 从根结点（0）出发
        for (int i = 0; str[i]; ++i) {
            if (ch[p] == NULL) {
                ch[p] = new int[MAX_C];  // 只有 p 当包含子结点的时候才去开辟 ch[p] 的空间
                memset(ch[p], -1, sizeof(int) * MAX_C);  // 初始化为 -1
            }
            if (ch[p][str[i] - 'a'] == -1) {  // 该子结点不存在
                ch[p][str[i] - 'a'] = ++tot;  // 新增结点
            } 
            p = ch[p][str[i] - 'a'];  // 在 Trie 树上继续插入字符串 str
        }
        cnt[p]++;
    }

    int find(char *str) {  // 返回字符串 str 的出现次数
        int p = 0;
        for (int i = 0; str[i]; ++i) {
            if (ch[p][str[i] - 'a'] == -1) {
                return 0;
            }
            p = ch[p][str[i] - 'a'];
        }
        return cnt[p];
    }
};
```

### 32、全排列
函数形式
```c++
int a[10]={0,1,2,3,4,5,6,7};
do{
    int t = 0;
    for(int i=0;i<8;i++){
        t = t*10+a[i];
    }
    cout<<t<<endl;
}while(next_permutation(a,a+8));
```
dfs形式
```c++
#include<stdio.h>  
int n,a[10],book[10];//特别说明c语言全局变量没有赋值默认为 0,无需再次初始化；   
void dfs(int step)//step 表示当前在第几个位置   
{  
    int i;  
    if(step==n+1)//如果step==n+1表示前n个数字已经放好   
    {  
        //输出一种全排列   
        for(i=1;i<=n;i++)  
         printf("%d",a[i]);  
        printf("\n");  
       return;   
    }  
    //每次搜索都从1-n 一一尝试   
    for(i=1;i<=n;i++)  
    {  
        if(book[i]==0)//判断次数字是否用过   
        {  
            a[step]=i;//存储当前位置的数字，以便满足条件输出   
            book[i]=1;//当前数字已用过，改变标志，以防重用   
            dfs(step+1);//放好当前位置数字之后，安排下一个数字   
            book[i]=0;//回溯，当满足一种全排列后，进行下一种尝试   
        }  
    }  
    return ;  
}  
int main()  
{  
    scanf("%d",&n);//输入只能为1-9之间的整数，表示1-n的全排列   
    dfs(1);//从第一个位置开始   
    return 0;  
}  
```

### 33、01，完全，多重背包模板
```c++
#include<bits/stdc++.h>
using namespace std;

const int MAXN = 101;
const int SIZE = 50001;

int dp[SIZE];
int volume[MAXN], value[MAXN], c[MAXN];
int n, v;           //  总物品数，背包容量

//  01背包
void ZeroOnepark(int val, int vol)
{
    for (int j = v ; j >= vol; j--)
    {
        dp[j] = max(dp[j], dp[j - vol] + val);
    }
}

//  完全背包
void Completepark(int val, int vol)
{
    for (int j = vol; j <= v; j++)
    {
        dp[j] = max(dp[j], dp[j - vol] + val);
    }
}

//  多重背包
void Multiplepark(int val, int vol, int amount)
{
    if (vol * amount >= v)
    {
        Completepark(val, vol);
    }
    else
    {
        int k = 1;
        while (k < amount)
        {
            ZeroOnepark(k * val, k * vol);
            amount -= k;
            k <<= 1;
        }
        if (amount > 0)
        {
            ZeroOnepark(amount * val, amount * vol);
        }
    }
}

int main()
{
    while (cin >> n >> v)
    {
        for (int i = 1 ; i <= n ; i++)
        {
            cin >> volume[i] >> value[i] >> c[i];      //   费用，价值，数量
        }
        memset(dp, 0, sizeof(dp));
        for (int i = 1; i <= n; i++)
        {
            Multiplepark(value[i], volume[i], c[i]);
        }
        cout << dp[v] << endl;
    }
    return 0;
}
```

### 34、floyd算法

```c++
/*
样例输入 
5 12 
1 2 967 
2 3 900 
3 4 771 
4 5 196 
2 4 788 
3 1 637 
1 4 883 
2 4 82 
5 2 647 
1 4 198 
2 4 181 
5 2 665 
样例输出 
0 280 637 198 394 
280 0 853 82 278 
637 853 0 771 967 
198 82 771 0 196 
394 278 967 196 0
*/

#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int INF = 100000;

int d[105][1005];
int n;

int main(){
	freopen("input.txt","r",stdin);
	
	int n,m,u,v,cost;
	while(~scanf("%d %d",&n,&m)){
		memset(d,0,sizeof(d));
		for(int i=1;i<=n;i++){
			for(int j=1;j<=n;j++){
				if(i == j) d[i][j] = 0;
				else d[i][j] = INF;
			}
		}
		
		for(int i=1;i<=m;i++){
			scanf("%d %d %d",&u,&v,&cost);
			d[u][v] = d[v][u] = min(cost,d[u][v]);
		}
		
		for(int k=1;k<=n;k++){
			for(int i=1;i<=n;i++){
				for(int j=1;j<=n;j++){
					d[i][j] = min(d[i][j],d[i][k]+d[k][j]);
				}
			}
		}
		
		for(int i=1;i<=n;i++){
			for(int j=1;j<=n;j++){
				if(j!=n){
					printf("%d ",d[i][j]);
				}else{
					printf("%d\n",d[i][j]);
				}
			}
		}
	}
	
	return 0;
}
```

### 35、组合数
求解组合数 C (n, k) % p 的三种方法：

方法1(逆元求法)：

```c++
const int N = 1e5 + 10;  
const int MOD = 1e9 + 7;  
int f[N], finv[N], inv[N];  
   
void init(void) {　　　　//要求MOD是质数，预处理时间复杂度O(n)  
    inv[1] = 1;  
    for (int i=2; i<N; ++i) {  
        inv[i] = (MOD - MOD / i) * 1ll * inv[MOD%i] % MOD;  
    }  
    f[0] = finv[0] = 1;  
    for (int i=1; i<N; ++i) {  
        f[i] = f[i-1] * 1ll * i % MOD;  
        finv[i] = finv[i-1] * 1ll * inv[i] % MOD;  
    }  
}  
```

方法2：C(n,m)= C(n,n-m)= C(n-1,m-1)+C(n-1,m)
```c++
const int N = 2000 + 10;  
const int MOD = 1e9 + 7;  
int comb[N][N];  
   
void init(void) {　　　　//对MOD没有要求，预处理时间复杂度O(n^2)  
    for (int i=0; i<N; ++i) {  
        comb[i][i] = comb[i
        ][0] = 1;  
        for (int j=1; j<i; ++j) {  
            comb[i][j] = comb[i-1][j] + comb[i-1][j-1];  
            if (comb[i][j] >= MOD)  {  
                comb[i][j] -= MOD;  
            }  
        }  
    }  
}  
```

方法3(Lucas定理，大组合数取模， HDOJ 3037为例)：
```c++
ll f[N];  
void init(int p) {                 //f[n] = n!  
    f[0] = 1;  
    for (int i=1; i<=p; ++i) f[i] = f[i-1] * i % p;  
}  
   
ll pow_mod(ll a, ll x, int p)   {  
    ll ret = 1;  
    while (x)   {  
        if (x & 1)  ret = ret * a % p;  
        a = a * a % p;  
        x >>= 1;  
    }  
    return ret;  
}  
   
ll Lucas(ll n, ll k, int p) {       //C (n, k) % p  
     ll ret = 1;  
     while (n && k) {  
        ll nn = n % p, kk = k % p;  
        if (nn < kk) return 0;                   //inv (f[kk]) = f[kk] ^ (p - 2) % p  
        ret = ret * f[nn] * pow_mod (f[kk] * f[nn-kk] % p, p - 2, p) % p;  
        n /= p, k /= p;  
     }  
     return ret;  
}  
   
int main(){  
    init (p);  
    printf ("%I64d\n", Lucas (n + m, n, p));  
   
    return 0;  
}  
```