#### query ORM 프로젝트

IQueryBuilder_SQL.php
```
<?php

interface SQL
{
    public function from($tableName);

    public function into($tableName);

    public function columns();

    public function insert($values);

    public function select($fields);

    public function where($field);

    public function orderBy($field, $sortOrder='DESC');

    public function isIn($fields);

    public function update($tableName);

    public function set($field, $value, $delimiter='');

    public function limit($start, $end='');

    public function innerJoin();
}
```

QueryBuilder_Table.php
```
<?php
class Table
{
    public function join(array $args){
        if (count($args) >= 4){
             $sql = " AS $args[0] $args[3] $args[1] $args[2]";
        }else {
             $sql = " $args[3] $args[1] AS $args[2]";
        }
        return $sql;
    }
}

```

MYSQL.php
```
<?php


class MYSQL extends Table implements SQL
{
    public $sql;

    public function from($tableName)
    {
        $this->sql = "SELECT fields FROM ${tableName}";
        return $this;
    }

    public function into($tableName)
    {
        $this->sql = "INSERT INTO ${tableName}";
        return $this;
    }

    public function columns()
    {
        $fields = implode(", ", func_get_args());
        $this->sql .= "(${fields})";
        return $this;
    }

    public function insert($values)
    {
        $values = implode(", ", func_get_args());
        $this->sql .= " VALUES(${values})";
        return $this;
    }

    public function select($fields)
    {
        $fields = implode(", ", func_get_args());
        $this->sql = str_replace('fields', $fields, $this->sql);
        return $this;
    }

    public function where($field)
    {
        $this->sql .= " WHERE ${field}";
        return $this;
    }

    public function orderBy($field, $sortOrder='DESC')
    {
        $this->sql .= " ORDER BY ${field} ${sortOrder}";
        return $this;
    }

    public function isIn($fields)
    {
        $fields = implode(", ", func_get_args());
        $this->sql .= " IN(${fields})";
        return $this;
    }

    public function update($tableName)
    {
        $this->sql .= "UPDATE ${tableName} SET";
        return $this;
    }

    public function set($field, $value, $delimiter='')
    {
        $this->sql .= " ${field}=${value}$delimiter";
        return $this;
    }

    public function limit($start, $end='')
    {
        if (!empty($start)){
            $this->sql .= " LIMIT ${start}";
        }
        if (!empty($end)){
            $this->sql .= ", ${$end}";
        }
        return $this;
    }

    public function innerJoin()
    {
        $args = func_get_args();
        array_push($args, 'INNER JOIN');
        $this->sql .= $this->join($args);
        return $this;
    }

    public function leftJoin()
    {
        $args = func_get_args();
        array_push($args, 'LEFT OUTER JOIN');
        $this->sql .= $this->join($args);
        return $this;
    }

    public function On()
    {
        $args = func_get_args();
        $this->sql .= " ON $args[0] = $args[1]";
        return $this;
    }
}

function SqlCount($field){
    return "COUNT(${field})";
}

function SqlSum($field){
    return "SUM(${field})";
}
```

```
$queryBuild = (new MYSQL())
                   ->from('user')
                   ->select('id', 'no')
                   ->where("id='{$id}'");
// select id, no from user where id='test';
$tmp->fetch_array($queryBuid); 
```
