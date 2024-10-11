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

- 풀이 2 :