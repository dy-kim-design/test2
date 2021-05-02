# test2
tutorial repository

# 테이블 형식 추출 임의 쿼리

SELECT
    t1.table_name, ORDINAL_POSITION, column_nam 'Column Name', COLUMN_TYPE 'COLUMN TYPE', column_key 'Key', case
when is_nullable = 'YES' THEN 'Y'
    when is_nullable = 'NO' THEN 'N'
   END AS 'Null able',
   column_default 'Default Value', column_comment 'Comment', t1.table_comment, extra 'Extra'
FROM
   (SELECT
        table_name, table_comment
    FROM
        information_schema.TABLES WHERE table_schema = 'db_query') t1,
    (SELECT
        table_name, ORDINAL_POSITION, column_name, COLUMN_TYPE, column_key, extra, is_nullable, column_default, column_comment
    FROM
        information_schema.COLUMNS WHERE table_schema = 'db_query') t2
WHERE
    t1.table_name = t2.table_name
ORDER BY
    t1.table_name, ordinal_position;
