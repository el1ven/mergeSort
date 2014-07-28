1.归并排序算法是采用分治法的一个非常典型的应用。归并排序的思想是将一个数组中的数都分成单个的；对于单独的一个数，它肯定是有序的，然后，我们将这些有序的单个数在合并起来，组成一个有序的数列。这就是归并排序的思想。它的时间复杂度为O(N*logN)。


2.关于问题图片中的left＋r而不是r的原因？
因为我们要把tmp复制到个个小数组当中去，而小树组的首地址就是left，用相对位置的方法。

3.代码：

\#include \<iostream>

\#include \<cstring>

\#include \<cmath>

\#include \<cstdlib>

\#include \<algorithm>


using namespace std;

//将两个有序数列a[left,mid]和a[mid,right]进行合并

void mergeArray(int a[], int left, int mid, int right, int temp[]){
    
    int i = left;
    int j = mid + 1;
    int m = mid;
    int n = right;
    int k = 0;
    
    while(i <= m && j<= n){
        if(a[i] <= a[j]){
            temp[k++] = a[i++];
        }else{
            temp[k++] = a[j++];
        }
    }
    
    while(i <= m){//如果左边有剩余元素，则都是大的，直接接到队尾
        temp[k++] = a[i++];
    }
    
    while(j <= n){//如果右边有剩余元素，则都是大的，直接接到队尾
        temp[k++] = a[j++];
    }
    
    for(int r = 0; r < k ; r++){
        a[left + r] = temp[r];//得到合并后的数组
    }
}

void mergeSort(int a[], int left, int right, int temp[]){

    if(left < right){//此处无等号，就一个元素就不用排序
        int mid = (left +right)/2;
        mergeSort(a,left,mid,temp);//左边有序
        mergeSort(a,mid+1,right,temp);//右边有序
        mergeArray(a,left, mid, right, temp);//将两个有序的合并
        
    }
    
}


int main(){
    
    int n = 0;//数字的个数

    while(cin>>n){
        int arr[100] = {0};//初始化
        int temp[100] = {0};//中转数组
        for(int i = 0; i < n; i++){
            cin>>arr[i];
        }
        mergeSort(arr,0,n-1,temp);
        for(int j = 0 ; j < n; j++){
            cout<<arr[j]<<endl;
        }
    }
    return 0;
}
