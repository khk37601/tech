
php는 database 연결하는 방법은 여러방법이 있다

```
1. mysqli
2. pdo
```

사용예시)

```
namespace lab\database;

use PDO;
use Exception;

class DB
{
    protected $pdo;

    public function __construct($host, $dbname, $id, $pwd)
    {
        try {
            $this->pdo = new PDO(
                "mysql:host=" . $host .  ";dbname=" . $dbname,
                $id,
                $pwd
            );
            $this->pdo->exec('SET NAMES utf8');
            $this->pdo->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
            $this->pdo->setAttribute(PDO::ATTR_EMULATE_PREPARES, FALSE);
        } catch (Exception $e) {
            echo "죄송합니다 고객센터에 문의 바랍니다. :D";
            exit();
        }
    }
    .....
}
```

```
namespace lab/database/mariadb;

use lab\database;

class Mariadb extends DB
{
    public function __construct($host, $dbname, $id, $pwd)
    {
        parent::__construct($host, $dbname, $id, $pwd);
    }
}

class Postgresql extends DB
{
  ...
}

// RDBS 유형 별로 확장성이 가능하도록 설계.

```
