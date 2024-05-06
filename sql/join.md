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