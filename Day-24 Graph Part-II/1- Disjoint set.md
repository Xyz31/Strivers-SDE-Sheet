# Disjoint Set

```md 


```

```cpp


class DisjointSet{
    std::vector<int> usize,urank,parent;
public:
    DisjointSet(int n){
        usize.resize(n+1,1);
        urank.resize(n+1,0);
        parent.resize(n+1);
        for(int i=0;i<n;i++){
            parent[i] = i;
        }
    }

    //Parent()
    int findparent(int node){
        if(node == parent[node]){
            return node;
        }

        //normal
        //return findparent(parent[node]);

        //Path Compression below
        return parent[node] = findparent(parent[node]);
    }

    //Union by Rank()
    void unionbyRank(int u,int v){
        int ult_u = findparent(u);
        int ult_v = findparent(v);
        if(ult_u == ult_v)
            return;

        if(urank[ult_u] < urank[ult_v]){
            parent[ult_u] = ult_v;
        }
        else if(urank[ult_u] > urank[ult_v]){
            parent[ult_v] = ult_u;
        }
        else{
            parent[ult_v] = ult_u;
            urank[ult_u]++;
        }
    }

    // Union By Size()
    void unionbySize(int u,int v){
        int ult_u = findparent(u);
        int ult_v = findparent(v);
        if(ult_u == ult_v)
            return;

        if(urank[ult_u] < urank[ult_v]){
            parent[ult_u] = ult_v;
            usize[ult_v] += usize[ult_u];
        }
    
        else{
            parent[ult_v] = ult_u;
            usize[ult_u] += usize[ult_v];
        }
    }
};

int main(int argc, char const *argv[])
{
    DisjointSet ds(7);

    // Union by Rank
    /*
    ds.unionbyRank(1,2);
    ds.unionbyRank(3,2);
    ds.unionbyRank(4,2);
    ds.unionbyRank(6,5);
    ds.unionbyRank(7,6);
    if (ds.findparent(3) == ds.findparent(7))
    {
        cout<<"Same\n";
    }
    else{
        cout<<"Not Same\n";
    }
    ds.unionbyRank(2,4);
    if (ds.findparent(3) == ds.findparent(7))
    {
        cout<<"Same\n";
    }else{
        cout<<"Not Same";
    }

    */

    // Union by size()
    ds.unionbySize(1,2);
    ds.unionbySize(3,2);
    ds.unionbySize(4,2);
    ds.unionbySize(6,5);
    ds.unionbySize(7,6);
    if (ds.findparent(3) == ds.findparent(7))
    {
        cout<<"Same\n";
    }
    else{
        cout<<"Not Same\n";
    }
    ds.unionbySize(6,4);
    if (ds.findparent(3) == ds.findparent(7))
    {
        cout<<"Same\n";
    }else{
        cout<<"Not Same";
    }
    return 0;
}

```