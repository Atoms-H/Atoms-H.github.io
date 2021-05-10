### Welcome to My Pages

Hi! This is AtomsH.
(You may ask why I am called this name. Emmm... There seems to be some reasons, but I'm not going to tell you :)
My native language is not English, so I might make a grammatical mistake.
(好了，英语不会了，写不下去了，用中文+-+)

## 🎲本周学习任务：线段树

### 模版
查找区间最大值
```markdown
#include <bits/stdc++.h>
using namespace std;

//struct数组存储线段树
struct SegmentTree
{
    int l,r;
    int dat;
}t`[N*2]`;

//建树
void build(int p,int l,int r)//当前节点，节点代表的区间[l,r]
{
    t[p].l=l,t[p].r=r;//节点p表示区间[l,r]
    if(l==r)//叶节点
    {
        t[p].dat=a[l];
        return;
    }
    int mid=(l+r)/2;
    build(p * 2,l,mid);//建立左子树
    build(p * 2+1,mid+1,r);//建立右子树
    t[p].dat=max(t[p * 2].dat,t[p * 2+1].dat);//从下往上传递信息
}

//单点修改
void change(int p,int x,int v)//当前节点，需要更新[x,x]区间为v
{
    if(t[p].l==t[p].r)//找到[x,x]区间
    {
        t[p].dat=v;
        return;
    }
    int mid=（t[p].l+t[p].r)/2;
    if(x<=mid) change(p * 2,x,v);//x属于左半区间
    else change(p * 2+1,x,v);//x属于右半区间
    t[p].dat=max(t[p * 2].dat,t[p * 2+1].dat);//从下往上更新
}

//区间查询
int ask(int p,int l,int r)//当前节点，查找[l,r]
{
    if(l<=t[p].l&&r>=t[p].r) return t[p].dat;//当前区间包含要查找的区间
    int mid=(t[p].l+t[p].r)/2;
    int val=-0x3f3f3f3f;
    if(l<=mid) val=max(val,ask(p * 2,l,r));//和左子节点有重合
    if(r>mid) val=max(val,ask(p * 2+1,l,r));//和右子节点有重叠
    return val;
}

int main()
{
    int n;//区间
    build(1,1,n);
    change(1,x,v);
    ask(1,l,r);
}

```
