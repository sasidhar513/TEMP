#include<bits/stdc++.h>
using namespace std;
int check[1000][1000];
pair<int , int >comparePair(pair<int,int> out1, pair<int,int > out2){
    if(out1.second>out2.second)
        return out1;
    else if(out1.second== out2.second){
        if(out1.first>0&&out2.first<0)
            return out2;
        else if(out2.first>0&&out1.first<0)
            return out1;
        else if(out2.first>0&&out1.first>0&&out1>out2)
            return out2;
        else
            return out1;           
    }
    else
        return out2;        
}
pair<int ,int> getMinPointsUtil(int i, int j, int n, int arr[1000][1000]){
    if(i==n-1&&j==n-1)
    {
        return make_pair(arr[i][j],arr[i][j]);
    } 
    pair<int,int> out1,out2;
    if(j+1<n){
        pair<int,int> min1=getMinPointsUtil(i, j+1, n, arr);
        int second=0;
        if(min1.second<0)
            second=min1.second+arr[i][j];
        else 
            second=arr[i][j];
        int first= min1.first+arr[i][j];
        out1=make_pair(first,second);
    }  
    if(i+1<n){
        pair<int,int> min1=getMinPointsUtil(i, j+1, n, arr);
        int second=0;
        if(min1.second<0)
            second=min1.second+arr[i][j];
        else 
            second=arr[i][j];
        int first= min1.first+arr[i][j];
        out2=make_pair(first,second);
    } 
    return comparePair(out1,out2);         
}
int getMinPoints(int n, int arr[1000][1000]){
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            check[i][j]=-1;
     getMinPointsUtil(0,0,n,arr);
    return 2;
    
}
int main(){
    int tc;
    cin>>tc;
    while(tc-->0){
        int n;
        cin>>n;
        int arr[1000][1000];
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                cin>>arr[i][j];
        cout<<getMinPoints( n, arr)<<endl;
    }
}
/*
1
3
-2 -3 3 -5 -10 1 10 30 -5


*/
