# decorator

## 1.Версия

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
