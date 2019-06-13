SQL 查询重复出现次数最多的记录，按出现频率排序\(SQL语句\)

    SELECT DISTINCT count( * ) AS count,journal_id FROM `car_journal_praise`  WHERE status = 1 GROUP BY journal_id  ORDER BY count DESC LIMIT 10"



