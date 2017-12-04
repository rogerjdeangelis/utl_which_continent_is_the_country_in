# utl_which_continent_is_the_country_in
Which continent is the country in?
    Which continent is the country in?

    github
    https://github.com/rogerjdeangelis/utl_which_continent_is_the_country_in

    see
    https://goo.gl/GJRHF8
    https://stackoverflow.com/questions/47510141/get-continent-name-from-country-name-in-r

    markus profile
    https://stackoverflow.com/users/8583393/markus

    INPUT

      SD1.HAVE total obs=53  |    RULE
                             |
        COUNTRY              |  CONTINENT
                             |
        Afghanistan          |  Asia
        Albania              |  Europe
        Algeria              |  Africa
        Burundi              |  Africa
        Cambodia             |  Asia
        Cameroon             |  Africa
        Canada               |  Americas
        Chad                 |  Africa
        ...


    WORKING CODE
    ============
        have$continent<-countrycode(sourcevar=have$COUNTRY,origin="country.name",destination="continent");

    OUTPUT
    ======
       WORK.WANT total obs=53

        COUNTRY        CONTINENT

        Afghanistan    Asia
        Albania        Europe
        Algeria        Africa
        Burundi        Africa
        Cambodia       Asia
        Cameroon       Africa
        Canada         Americas
        Chad           Africa
        Iceland        Europe
       ....

    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
    informat country $24.;
    input country;
    cards4;
    Afghanistan
    Albania
    Algeria
    Burundi
    Cambodia
    Cameroon
    Canada
    Chad
    Iceland
    India
    Indonesia
    Iran
    Israel
    Italy
    Jamaica
    Japan
    Jordan
    Kazakhstan
    Kenya
    Morocco
    Mozambique
    Namibia
    Nauru
    Nepal
    Netherlands
    Nicaragua
    Niger
    Nigeria
    Norway
    Oman
    Pakistan
    Palau
    Panama
    Paraguay
    Peru
    Philippines
    Poland
    Portugal
    Qatar
    Romania
    Rwanda
    Samoa
    Tunisia
    Turkey
    Turkmenistan
    Tuvalu
    Uganda
    Ukraine
    Venezuela
    Vietnam
    Yemen
    Zambia
    Zimbabwe
    ;;;;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname sd1 sas7bdat "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk sas7bdat "%sysfunc(pathname(work))";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(haven);
    library(countrycode);
    have<-read_sas("d:/sd1/have.sas7bdat");
    have$continent<-countrycode(sourcevar = have$COUNTRY, origin = "country.name", destination = "continent");
    endsubmit;
    import r=have data=wrk.want;
    run;quit;
    ');
