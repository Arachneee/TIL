최장 증가 부분 수열

- 풀이 1 : dp O(n^2)
	-  dp[k] : k번째 수로 끝나면서 최장 길이 수

```
int[] arr = new int[n];  
  
for (int i = 0; i < n; i++) {  
    arr[i] = Integer.parseInt(br.readLine());  
}  
  
int[] dp = new int[n];  
  
for (int i = 0; i < n; i++) {  
    dp[i] = 1;  
    for (int j = 0; j < i; j++) {  
        if (arr[i] > arr[j]) {  
            dp[i] = Math.max(dp[i], dp[j] + 1);  
        }  
    }  
}  
int asInt = Arrays.stream(dp).max().getAsInt();
```

- 풀이 2 : 이분 탐색 O(nlogn)
	- LIS[] : 최장 증가 부분 수열을 의미하지 않는다. 길이만 유효하다.
```
int[] arr = new int[n];  
  
for (int i = 0; i < n; i++) {  
    arr[i] = Integer.parseInt(br.readLine());  
}  
  
int[] lis = new int[n];  
Arrays.fill(lis, Integer.MAX_VALUE);  
  
lis[0] = arr[0];  
int count = 1;  
for (int i = 1; i < n; i++) {  
    int now = arr[i];  
  
    if (lis[count - 1] < now) {  
        lis[count++] = now;  
        continue;  
    }  
    if (lis[0] > now) {  
        lis[0] = now;  
        continue;  
    }  
  
    int left = 0;  
    int right = count;  
  
    while (left + 1 < right) {  
        int mid = (left + right) / 2;  
        if (now > lis[mid]) {  
            left = mid;  
        } else {  
            right = mid;  
        }  
    }  
    lis[right] = now;  
}
```