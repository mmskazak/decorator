# decorator

## 1.Вариант

    /*Реалтзация*/  
    interface ДанныеДокумента  
    {  
      public function вернутьДанныеДокумента(): array  		
    }  


    abstract class ДанныеДокументДеократор implements ДанныеДокумента
    {
      protected классДерократор;

      public function __construct(Model $ДАННЫЕ, ДанныеДокумента $классДерократор)
      {
        $this->классДерократор = $классДерократор;
      }

      public function вернутьДанныеДокумента(): array
      {
        return array_merge($this->классДерократор->вернутьДанныеДокумента, $ДАННЫЕ);
      }

    }


    /*Класс под определенную  сущность*/
    class ДанныеДокументДеократорА extends ДанныеДокументДеократор
    {
    protected классДерократор;
     
      public function __construct(EntityModel $ДАННЫЕ, ДанныеДокумента $классДерократор)
      {
          parent::__construct(Model $ДАННЫЕ, ДанныеДокумента $классДерократор)
      } 
    }
      


    class ПервыйДокумент implements ДанныеДокумента
    {
      public function __construct(array $данные)	

      public function вернутьДанныеДокумента(): array
      {
        return $данные;
      }
    }


    /*Пример*/  
    //это если этот класс был бы не астрактным
    $данныеНаЛист = new ДанныеДокументДеократор(SIGNATURIES,new ПервыйДокумент($DOCUMENT))


    /*Документ*/  
    class Type14
    {
      return new ДанныеДокументДеократорA(SIGNATURIES,new ПервыйДокумент($DOCUMENT))
    }



    /*Документ*/  
    class Type15
    {
      return new ДанныеДокументДеократорБ($ДАННЫЕ, new ДанныеДокументДеократорА($SIGNATURIES,new ПервыйДокумент($DOCUMENT));
    }
    
    
   ## 2.Вариант


    /*Клиент*/
    $стекло = new Пленка(new Закалка(new Резка(new Стекло())));
    $затрачено_времени = $стекло->затраченоВремени(); // 0 + 120 + 60 + 90 = 270 сек 

    /*Реализация*/
    interface Время
    {
        public function затраченоВремени(): int
    }

    /*Исходный объект - он будет декарироваться*/
    class Стекло implements Время
    {
        public function затраченоВремени(): int
        {
            return 0; //сек
        }
    }

    abstract class CтеклоДекоратор implements Время
    {

        protected $время;

        public function __construct(Время $время)
        {
            $this->время = $время;
        }

        public function затраченоВремени(): int
        {
            return $this->время->затраченоВремени();
        }
    }

    /*Декоратор(обертка)*/
    class Резка extends CтеклоДекоратор 
    {
        public function затраченоВремени(): int
        {
             return $this->время->затраченоВремени() + 120сек;
        }
    }

    /*Декоратор(обертка)*/
    class Закалка extends CтеклоДекоратор 
    {
        public function затраченоВремени(): int
        {
             return $this->время->затраченоВремени() + 60сек;
        }
    }

    /*Декоратор(обертка)*/
    class Пленка extends CтеклоДекоратор 
    {
        public function затраченоВремени(): int
        {
             return $this->время->затраченоВремени() + 90сек;
        }
    }
    
   ## 3.Вариант
    
    interface IGetData {
      /**
       * Делает запрос на внешний API и
       * возвращает результат в виде массива.
       *
       * @param array $request
       * @return array
       */
      public function getResponseData(array $request): array;
    }


    class DataProvider implements IGetData {
      private string $host;
      private string $user; // User
      private string $password;

      /**
       * @param string $host
       * @param string $user
       * @param string $password
       */
      public function __construct(string $host, string $user, string $password) {
        $this->host = $host;
        $this->user = $user;
        $this->password = $password;
      }

          /**
           * @param array $request
           * @return array
           */
          public function getResponseData(array $request): array {
            //запрос данных
            //возвращается фейковый массив
            return [$this->host, $this->user, $this->password];
          }
        }


        class BaseDecorator implements IGetData {

          protected IGetData $data;

          public function __construct(IGetData $data) {
            $this->data = $data;
          }

          public function getResponseData(array $request): array {
            return $this->data->getResponseData($request);
          }

        }

        class CacheDataDecorator extends BaseDecorator {

          protected CacheItemPoolInterface $cache;

          public function __construct(IGetData $data, CacheItemPoolInterface $cache) {
            parent::__construct($data);
            $this->cache = $cache;
          }

          /**
           * @param array $request
           * @return array
           */
          public function getResponseData(array $request): array {

            $responseArray = $this->data->getResponseData($request);
            //Создание кеша
            //$this->cache->
            return $responseArray;
          }

        }


        class LoggerDecorator extends BaseDecorator {

          protected LoggerInterface $logger;

          public function __construct(IGetData $data, LoggerInterface $logger) {
            parent::__construct($data);
            $this->logger = $logger;
          }

          /**
           * @param array $request
           * @return array
           */
          public function getResponseData(array $request): array {

            $responseArray = $this->data->getResponseData($request);
            //Логирование
            //$this->logger->
            return $responseArray;
          }
        }


        class Client {

          /**
           * @param CacheItemPoolInterface $cache
           * @param LoggerInterface $logger
           */
          public function doSomeTask(CacheItemPoolInterface $cache,LoggerInterface $logger): void {
            $dataProvider = new DataProvider('https://api.something.ru/v2/something', 'misha', 'password');
            $baseDecorator = new BaseDecorator($dataProvider);
            $cacheDataDecorator = new CacheDataDecorator($baseDecorator, $cache);
            $loggerDecorator = new LoggerDecorator($cacheDataDecorator, $logger);
            $loggerDecorator->getResponseData();
          }
        }

