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
