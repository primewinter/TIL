## 오라클

### ORDER BY DECODE(컬럼명, '값', 순서)

```sql
ORDER BY DECODE(GRADE, 'S', 0, 'A', 1, 'B', 2, 'C', 3);
```

## PostgreSQL / MySQL

### ORDER BY CASE WHEN ... THEN ... END

```sql
ORDER BY  CASE 
            WHEN COL1 LIKE 'A%' THEN 0 
            WHEN COL2 LIKE 'B%' THEN 1
          END
```
