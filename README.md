# utl-interesting-uses-of-macro-function-syscall-with-sas-call-routines
Interesting uses of macro function syscall with sas call routines
    Interesting uses of macro function syscall with sas call routines

    github
    https://tinyurl.com/regyvgl
    https://github.com/rogerjdeangelis/utl-interesting-uses-of-macro-function-syscall-with-sas-call-routines

    You need this macro for checking

    %macro dosubl(arg);
      %let rc=%qsysfunc(dosubl(&arg));
    %mend dosubl;



    SAS Forum
    https://communities.sas.com/t5/SAS-Programming/How-to-use-syscall-scan/m-p/632558

    Patrick
    https://communities.sas.com/t5/user/viewprofilepage/user-id/12447

    These SAS call routines can be used with syscall and macro variables

      call missing  (set mutiple macro variables to missing)
      call missing  (set mutiple macro variable to 0)
      call set
      call scan
      call sortn and call sortc
      call stdize  ** I could not get any of the options like setting all macro variables to work;
      call tanh
      call logistic
      call softmax


    These are suppose to  work but I cannot get them to work;

    https://tinyurl.com/v8o46vm
    https://documentation.sas.com/?docsetId=lefunctionsref&docsetTarget=p07c8e0ktns1c7n1vtowjev5g724.htm&docsetVersion=9.4&locale=en#n05kaiyz3cameon1w489gi64npdk

       %syscall(%str(mult=),0,a,b,c)  * set macro vars to 0;

       %syscall(CALL COMPCOST Routine
       %syscall(call LEXCOMB Function
       %syscall(call LEXPERK Function
       %syscall(CALL LEXPERM Routine
       %syscall(CALL PRXCHANGE Routine
       %syscall(CALL PRXNEXT Routine
       %syscall(CALL PRXSUBSTR Routine


    *          _ _             _         _
      ___ __ _| | |  _ __ ___ (_)___ ___(_)_ __   __ _
     / __/ _` | | | | '_ ` _ \| / __/ __| | '_ \ / _` |
    | (_| (_| | | | | | | | | | \__ \__ \ | | | | (_| |
     \___\__,_|_|_| |_| |_| |_|_|___/___/_|_| |_|\__, |
                                                 |___/
    ;

    * set several macro variables to missing;

    %utlnopts; * turn logging off except put statements;

    options missing='.';

    %let total=100;
    %let wages=100000;
    %let name=roger;

    %syscall missing(total,wages,name);

    %put &=total;
    %put &=wages;
    %put &=name ;

    TOTAL=.
    WAGES=.
    NAME=

    *          _ _             _         _
      ___ __ _| | |  _ __ ___ (_)___ ___(_)_ __   __ _   _______ _ __ ___
     / __/ _` | | | | '_ ` _ \| / __/ __| | '_ \ / _` | |_  / _ \ '__/ _ \
    | (_| (_| | | | | | | | | | \__ \__ \ | | | | (_| |  / /  __/ | | (_) |
     \___\__,_|_|_| |_| |_| |_|_|___/___/_|_| |_|\__, | /___\___|_|  \___/
                                                 |___/
    ;

    options missing='.';

    %let total=100;
    %let wages=100000;
    %let name=roger;

    * change all to missing;
    %syscall missing(total,wages,name);

    options missing='0';
    %syscall missing(total,wages,name);
    options missing='.';

    %put &=total;
    %put &=wages;
    %put &=name ;

    /*
    TOTAL=0
    TOTAL=0
    WAGES=0
    NAME=
    */

    * check;
    %let s=&total * 99;
    %let res=%eval(&s);
    %put &=res;

    RES=0


    *          _ _            _
      ___ __ _| | |  ___  ___| |_
     / __/ _` | | | / __|/ _ \ __|
    | (_| (_| | | | \__ \  __/ |_
     \___\__,_|_|_| |___/\___|\__|

    ;

    * create a mdv macro datavector with macoro names and valuess
      for observation 5 in sashelp.class;

    %symdel dsid name sex age height weight /nowarn;

    %let dsid=%sysfunc(open(class, i));
    %put &=dsid;
    %syscall set(dsid);
    %let rc=%sysfunc(fetchobs(&dsid, 5));
    %let rc=%sysfunc(close(&dsid));


    %put &=name;
    %put &=age;
    %put &=sex;
    %put &=height;
    %put &=weight;

    DSID=1

    NAME=Joyce
    AGE=11
    SEX=F
    HEIGHT=51.3
    WEIGHT=50.5

    *          _ _
      ___ __ _| | |  ___  ___ __ _ _ __
     / __/ _` | | | / __|/ __/ _` | '_ \
    | (_| (_| | | | \__ \ (_| (_| | | | |
     \___\__,_|_|_| |___/\___\__,_|_| |_|

    ;

    * extract my first name from Mr Roger DeAngelis;

    %utlnopts;

    %let string=Mr Roger DeAngelis;

    %let cnt=2;
    %let pos=0;
    %let len=0;

    %syscall SCAN(string, cnt, pos, len );

    %let firstname=%substr(&string,&pos,&len);

    %put &=cnt ;
    %put &=pos ;
    %put &=len ;

    %put &=firstname;

    CNT=2
    POS=4

    LEN=5
    FIRSTNAME=Roger

    *          _ _       _      _ _
      ___ __ _| | |  ___| |_ __| (_)_______
     / __/ _` | | | / __| __/ _` | |_  / _ \
    | (_| (_| | | | \__ \ || (_| | |/ /  __/
     \___\__,_|_|_| |___/\__\__,_|_/___\___|

    ;

    %utlnopts;


    %utlnopts;

    %symdel w x y z / nowarn;

    %let w=1;
    %let x=2;
    %let y=3;
    %let z=4;

    %syscall stdize(w,x,y,z);

    %put &=w;
    %put &=x;
    %put &=y;
    %put &=z;

    /*
    W=-1.16189500386222
    X=-0.38729833462074
    Y= 0.38729833462074
    Z= 1.16189500386222
    */

    CHECK

    %dosubl('data;
             mean=mean(-1.16189500386222 ,-0.38729833462074 ,0.38729833462074 ,1.16189500386222 );
             std=std( -1.16189500386222 ,-0.38729833462074 ,0.38729833462074 ,1.16189500386222 );
             put mean= std=;
    run;quit;');

    MEAN=0 STD=1


    *          _ _                  _
      ___ __ _| | |  ___  ___  _ __| |_
     / __/ _` | | | / __|/ _ \| '__| __|
    | (_| (_| | | | \__ \ (_) | |  | |_
     \___\__,_|_|_| |___/\___/|_|   \__|

    ;

    %utlnopts; * turn ops off;

    %symdel w x y z / nowarn;

    %let w=1;
    %let x=3;
    %let y=2;
    %let z=04;


    %syscall sortn(w,x,y,z);

    %put &=w;
    %put &=x;
    %put &=y;
    %put &=z;

    /*
    W=1
    X=2
    Y=3
    Z=4
    */


    %let w=c;
    %let x=a;
    %let y=d;
    %let z=b;


    %syscall sortc(w,x,y,z);

    %put &=w;
    %put &=x;
    %put &=y;
    %put &=z;

    /*
    W=a
    X=b
    Y=c
    Z=d
    */

    %utlopts; * turn opts back on;


    *          _ _                               _
      ___ __ _| | |  _ __ __ _ _ __  _   _ _ __ (_)
     / __/ _` | | | | '__/ _` | '_ \| | | | '_ \| |
    | (_| (_| | | | | | | (_| | | | | |_| | | | | |
     \___\__,_|_|_| |_|  \__,_|_| |_|\__,_|_| |_|_|

    ;

    %let seed=1234;
    %let x=.;

    %syscall ranuni(seed,x);

    %put &=seed;
    %put &=x;

    * Random uniform variate;

    X=0.24381116043953

    *          _ _   _              _
      ___ __ _| | | | |_ __ _ _ __ | |__
     / __/ _` | | | | __/ _` | '_ \| '_ \
    | (_| (_| | | | | || (_| | | | | | | |
     \___\__,_|_|_|  \__\__,_|_| |_|_| |_|

    ;

    * hyperbolic tangent;

    %let x=0.5;
    %let y=-0.5;

    %syscall tanh(x, y);

    %put &=x ;
    %put &=y;

    X=0.46211715726
    Y=-0.46211715726

    %dosubl('data;
              x=tanh(.5);
              y=tanh(-.5);
              put x= / y= /;
            run;quit;
            ');

    X=0.4621171573
    Y=-0.462117157


    *          _ _   _             _     _   _
      ___ __ _| | | | | ___   __ _(_)___| |_(_) ___
     / __/ _` | | | | |/ _ \ / _` | / __| __| |/ __|
    | (_| (_| | | | | | (_) | (_| | \__ \ |_| | (__
     \___\__,_|_|_| |_|\___/ \__, |_|___/\__|_|\___|
                             |___/
    ;


    %let x=0.5;
    %let y=-0.5;

    %syscall logistic(x, y);

    %put &=x;
    %put &=y;


    x=exp(.5)/(1+exp(.5)) = 62245933120185;
    y=exp(-.5)/(1+exp(-.5)) = 0.37754066879814;

    *          _ _              __ _
      ___ __ _| | |  ___  ___  / _| |_ _ __ ___   __ ___  __
     / __/ _` | | | / __|/ _ \| |_| __| '_ ` _ \ / _` \ \/ /
    | (_| (_| | | | \__ \ (_) |  _| |_| | | | | | (_| |>  <
     \___\__,_|_|_| |___/\___/|_|  \__|_| |_| |_|\__,_/_/\_\

    ;

    %let x=0.5;
    %let y=-0.5;

    %let z=1;

    %syscall softmax(x, y, z);

    %put &=x;
    %put &=y;
    %put &=z;


    X=0.33149896042409
    Y=0.12195165230972
    Z=0.54654938726617

