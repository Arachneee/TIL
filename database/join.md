- sql JOIN ON 절에 조건을 쓰면 조건에 맞는 행만 JOIN에 참여한다.
    - 서브 쿼리 대신 ON 절에 사용하여 서브쿼리 2번을 줄일 수 있다.
    ex) 
    ```sql
    SELECT
        rt.start_at,
        rt.id,
        r.id is not null AS already_booked
    FROM reservation_time AS rt
    LEFT JOIN
        (SELECT id, time_id
        FROM reservation
        WHERE date = ? AND theme_id = ?) AS r
        ON rt.id = r.time_id
    ORDER BY start_at
    ```

    ```sql
    SELECT
        rt.start_at,
        rt.id,
        r.id is not null AS already_booked
    FROM reservation_time AS rt
    LEFT JOIN reservation AS r
    ON rt.id = r.time_id AND r.date = ? AND r.theme_id = ?
    ORDER BY start_at
    ```

서브쿼리의 성능은 좋지 않고 성능을 예측하기 어렵다.
- 서브쿼리를 inner join으로 풀 수 있다.
```sql
select 
	w,
	(select count(1)
		from Waiting w2
		where w2.reservation = w.reservation and w2.id <= w.id)
from Waiting w
where w.member = :member
```

```sql
select w, count(1)
from Waiting w  
inner join Waiting w2  
on w.member = :member
and w.reservation = w2.reservation  
where w2.id <= w.id  
group by w.reservation
```
