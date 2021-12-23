# interviewbit--array--balance-array

**------> Question:**

Given an integer array A of size N. You need to count the number of special elements in the given array.

A element is special if removal of that element make the array balanced.

Array will be balanced if sum of even index element equal to sum of odd index element.



Problem Constraints
1 <= N <= 105

1 <= A[i] <= 109



Input Format
First and only argument is an integer array A of size N.



Output Format
Return an integer denoting the count of special elements.



Example Input
Input 1:

 A = [2, 1, 6, 4]
Input 2:

 A = [5, 5, 2, 5, 8]


Example Output
Output 1:

 1
Output 2:

 2


Example Explanation
Explanation 1:

 After deleting 1 from array : {2,6,4}
    (2+4) = (6)
 Hence 1 is the only special element, so count is 1
Explanation 2:

 If we delete A[0] or A[1] , array will be balanced
    (5+5) = (2+8)
 So A[0] and A[1] are special elements, so count is 2.
 
 
 **-------> Code 1:**
 
 int Solution::solve(vector<int> &v) {
  
    long long int sum=0,sume=0,sumo=0;
    int n=v.size();
    vector<long long int> ep(n),es(n),op(n),os(n);

    for(int i=0;i<n;i++){
        sum+=v[i];
        if(i%2==0){
            sume+=v[i];
            ep[i]=sume;
            op[i]=0;
        }else{
            sumo+=v[i];
            op[i]=sumo;
            ep[i]=0;
        }
    }

    sume=0;
    sumo=0;

    for(int i=n-1;i>=0;i--){
        if(i%2==0){
            sume+=v[i];
            es[i]=sume;
            os[i]=0;
        }else{
            sumo+=v[i];
            os[i]=sumo;
            es[i]=0;
        }
    }

    long long int sumc=0,temp=sum;
    int count=0;

    for(int i=0;i<n;i++){
        temp=sum;
        temp-=v[i];

        if(temp%2!=0){
            continue;
        }

        temp/=2;
        if(i>0 && i<n-1){
            if(i%2!=0){
                sumc=es[i+1]+(op[i]-v[i]);
            }else{
                sumc=os[i+1]+(ep[i]-v[i]);
            }
        }else{
            if(i%2==0){
                sumc=sumo;
            }else{
                sumc=sume;
            }
        }

        if(sumc==temp){
            count++;
        }
    }

    return count;
}

                          
                          
**---------> Code 2:**
  
  int Solution::solve(vector<int> &v) {
  
    long long int sum=0,sume=0,sumo=0;
    int n=v.size();
     vector<long long int> v1(n);

     for(int i=0;i<n;i++){
         sum+=v[i];
         if(i%2==0){
             sume+=v[i];
             v1[i]=sume;
         }else{
             sumo+=v[i];
             v1[i]=sumo;
         }
     }

     long long int sumc=0,temp=sum;
     int count=0;

     for(int i=0;i<n;i++){
         temp=sum;
         temp-=v[i];

        if(temp%2!=0){
             continue;
        }

         temp/=2;
         if(i>0){
            if(i%2==0){
                 sumc=v1[i-2]+(sumo-v1[i-1]);
             }else{
                 sumc=v1[i-1]+(sumo-v1[i]);
             }
         }else{
             sumc=sumo;
         }

         if(sumc==temp){
             count++;
         }
     }

     return count;
}
  
  
  
  
 **------> Code 3:**
  
  int Solution::solve(vector<int> &A) {
  
    int n=A.size();
    if(n==1)
    return 1;
    if(n==2)
    return 0;
    int ans=0;
    vector<int>a(n);
    vector<int>b(n);
    if(n-1&1)
    {
        a[n-1]=A[n-1];
        b[n-1]=0;
    }
    else
    {
        a[n-1]=0;
        b[n-1]=A[n-1];
    }
    for(int i=n-2;i>=0;i--)
    {
        if(i&1)
        {
            a[i]=A[i]+a[i+1];
            b[i]=b[i+1];
        }
        else{
            a[i]=a[i+1];
            b[i]=A[i]+b[i+1];
        }

    }
    int m=0,h=0;
    for(int i=0;i<n;i++)
    {
        int s=m;
        int t=h;
        if(i<=n-2)
        {
        s+=b[i+1];
        t+=a[i+1];}
        if(s==t)
        ans++;




        if(i&1)
        {
            m+=A[i];

        }
        else
        h+=A[i];

    }
    return ans;
}
