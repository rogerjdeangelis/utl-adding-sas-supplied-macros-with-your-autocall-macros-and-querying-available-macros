# utl-adding-sas-supplied-macros-with-your-autocall-macros-and-querying-available-macros
    %let pgm=utl-adding-sas-supplied-macros-with-your-autocall-macros-and-querying-available-macros;

      Adding sas supplied macros with your autocall macros and querying available macros

      This elimiates appending macros and also provides a way to dudup macros or
      coose the macro you want to use.

      Process

        1 Copy all the indiviual macro and sas supplied macros into one directory
            c:/sasmacro

        2 Create fileref for the new sasautos folder
          filername sasautos "c:/sasmacro";

        3 Check for macro vailability using
           %put %sysfunc(ifc(%sysfunc(fileexist(c:/sasmacro/xpt2loc.sas))
            ,xpt2loc.sas exists
            ,xpt2loc.sas does not exist));

    github
    https://tinyurl.com/3azhbah4
    https://github.com/rogerjdeangelis/utl-adding-sas-supplied-macros-with-your-autocall-macros-and-querying-available-macros

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /*************************************************************************************************************************************/
    /*                                             |                                                                 |                   */
    /*                                             |                                                                 |                   */
    /*                   INPUT                     |       PROCESS (Copy all usaer and  sas macros to c:/sasmac)     | OUTPUT            */
    /*                                             |                                                                 |                   */
    /*  /*---- personal autocall library ----*/    | %macro robo(dircop);                                            | your personal     */
    /*  "c:\auto"                                  |                                                                 | autocall library  */
    /*                                             | data _null_;                                                    | combined with     */
    /*  /*---- sas supplied macros       ----*/    |  length rc cmd $200;                                            | sas macros        */
    /*                                             |  rc=dcreate("sasmacro","c:\");                                  |                   */
    /*  sasroot=                                   |  if upcase("&dircop") ="AUTO" then do;                          |                   */
    /*  C:\Program Files\sashome\SASFoundation\9.4 |     cmd=resolve(compbl('robocopy "c:\auto" c:\sasmacro /S'));   | Check xpt2loc.sas */
    /*                                             |     call system(cmd);                                           |                   */
    /*  "&SASROOT.\core\sasmacro"                  |  end;                                                           | xpt2loc.sas exists*/
    /*  "&SASROOT.\stat\sasmacro"                  |  else do;                                                       |                   */
    /*  "&SASROOT.\aacomp\sasmacro"                |    cmd=resolve(compbl('robocopy                                 | sasautos assigned */
    /*  "&SASROOT.\accelmva\sasmacro"              |   "C:\Program Files\sashome\SASFoundation\9.4\&dircop\sasmacro" |    to c:/sasmacro */
    /*  "&SASROOT.\access\sasmacro"                |     c:\sasmacro /S'));                                          |                   */
    /*  "&SASROOT.\assist\sasmacro"                |    call system(cmd);                                            |                   */
    /*  "&SASROOT.\dmscore\sasmacro"               |  end;                                                           |                   */
    /*  "&SASROOT.\eis\sasmacro"                   | run;quit;                                                       |                   */
    /*  "&SASROOT.\ets\sasmacro"                   | %mend robo;                                                     |                   */
    /*  "&SASROOT.\gis\sasmacro"                   |                                                                 |                   */
    /*  "&SASROOT.\graph\sasmacro"                 | %robo(auto);                                                    |                   */
    /*  "&SASROOT.\hps\sasmacro"                   | %robo(core);                                                    |                   */
    /*  "&SASROOT.\iml\sasmacro"                   | %robo(aacomp);                                                  |                   */
    /*  "&SASROOT.\inttech\sasmacro"               | %robo(accelmva);                                                |                   */
    /*  "&SASROOT.\or\sasmacro"                    | %robo(access);                                                  |                   */
    /*                                             | %robo(assist);                                                  |                   */
    /*                                             | %robo(dmscore);                                                 |                   */
    /*                                             | %robo(eis);                                                     |                   */
    /*                                             | %robo(ets);                                                     |                   */
    /*                                             | %robo(gis);                                                     |                   */
    /*                                             | %robo(graph);                                                   |                   */
    /*                                             | %robo(hps);                                                     |                   */
    /*                                             | %robo(iml);                                                     |                   */
    /*                                             | %robo(inttech);                                                 |                   */
    /*                                             | %robo(stat);                                                    |                   */
    /*                                             |                                                                 |                   */
    /*                                             | C:\                                                             |                   */
    /*                                             | +-sasmacro                                                      |                   */
    /*                                             | |  mymacro,sas                                                  |                   */
    /*                                             | |  ...                                                          |                   */
    /*                                             | \  xpt2loc.sas                                                  |                   */
    /*                                             |                                                                 |                   */
    /*                                             |                                                                 |                   */
    /*                                             | Determine if macro                                              |                   */
    /*                                             | is available                                                    |                   */
    /*                                             |                                                                 |                   */
    /*                                             | %put %sysfunc(ifc(%sysfunc(fileexist(c:/sasmacro/xpt2loc.sas))  |                   */
    /*                                             |   ,xpt2loc.sas exists                                           |                   */
    /*                                             |   ,xpt2loc.sas does not exist));                                |                   */
    /*                                             |                                                                 |                   */
    /*                                             | filename sasautos ("c:/sasmacro")                               |                   */
    /*                                             |                                                                 |                   */
    /*                                             |                                                                 |                   */
    /*************************************************************************************************************************************/

    /*                         _     _
    / |     ___ ___  _ __ ___ | |__ (_)_ __   ___   _ __ ___   __ _  ___ _ __ ___  ___
    | |    / __/ _ \| `_ ` _ \| `_ \| | `_ \ / _ \ | `_ ` _ \ / _` |/ __| `__/ _ \/ __|
    | |_  | (_| (_) | | | | | | |_) | | | | |  __/ | | | | | | (_| | (__| | | (_) \__ \
    |_(_)  \___\___/|_| |_| |_|_.__/|_|_| |_|\___| |_| |_| |_|\__,_|\___|_|  \___/|___/
     _                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    /*************************************************************************************************************************************/
    /*                                                                                                                                   */
    /*                   INPUT                                                                                                           */
    /*                                                                                                                                   */
    /*  /*---- personal autocall library ----*/                                                                                          */
    /*  "c:\auto"                                                                                                                        */
    /*                                                                                                                                   */
    /*  /*---- sas supplied macros       ----*/                                                                                          */
    /*                                                                                                                                   */
    /*  sasroot=                                                                                                                         */
    /*  C:\Program Files\sashome\SASFoundation\9.4                                                                                       */
    /*                                                                                                                                   */
    /*  "&SASROOT.\core\sasmacro"                                                                                                        */
    /*  "&SASROOT.\stat\sasmacro"                                                                                                        */
    /*  "&SASROOT.\aacomp\sasmacro"                                                                                                      */
    /*  "&SASROOT.\accelmva\sasmacro"                                                                                                    */
    /*  "&SASROOT.\access\sasmacro"                                                                                                      */
    /*  "&SASROOT.\assist\sasmacro"                                                                                                      */
    /*  "&SASROOT.\dmscore\sasmacro"                                                                                                     */
    /*  "&SASROOT.\eis\sasmacro"                                                                                                         */
    /*  "&SASROOT.\ets\sasmacro"                                                                                                         */
    /*  "&SASROOT.\gis\sasmacro"                                                                                                         */
    /*  "&SASROOT.\graph\sasmacro"                                                                                                       */
    /*  "&SASROOT.\hps\sasmacro"                                                                                                         */
    /*  "&SASROOT.\iml\sasmacro"                                                                                                         */
    /*  "&SASROOT.\inttech\sasmacro"                                                                                                     */
    /*  "&SASROOT.\or\sasmacro"                                                                                                          */
    /*                                                                                                                                   */
    /*************************************************************************************************************************************/

    %macro robo(dircop);

    data _null_;
     length rc cmd $200;
     rc=dcreate("sasmacro","c:\");
     if upcase("&dircop") ="AUTO" then do;
        cmd=resolve(compbl('robocopy "c:\auto" c:\sasmacro /S'));
        call system(cmd);
     end;
     else do;
       cmd=resolve(compbl('robocopy
      "C:\Program Files\sashome\SASFoundation\9.4\&dircop\sasmacro"
        c:\sasmacro /S'));
       call system(cmd);
     end;
    run;quit;
    %mend robo;

    %robo(auto);
    %robo(core);
    %robo(aacomp);
    %robo(accelmva);
    %robo(access);
    %robo(assist);
    %robo(dmscore);
    %robo(eis);
    %robo(ets);
    %robo(gis);
    %robo(graph);
    %robo(hps);
    %robo(iml);
    %robo(inttech);
    %robo(stat);

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Only a few hundred?                                                                                                    */
    /*                                                                                                                        */
    /* C:\                                                                                                                    */
    /* +-sasmacro                                                                                                             */
    /* |  mymacro,sas                                                                                                         */
    /* |  ...                                                                                                                 */
    /* \  xpt2loc.sas                                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___     ___     _____    __ _ _                __             _     _  ___
    |___ \   ( _ )   |___ /   / _(_) | ___ _ __ ___ / _|   _____  _(_)___| ||__ \
      __) |  / _ \/\   |_ \  | |_| | |/ _ \ `__/ _ \ |_   / _ \ \/ / / __| __|/ /
     / __/  | (_>  <  ___) | |  _| | |  __/ | |  __/  _| |  __/>  <| \__ \ |_|_|
    |_____|  \___/\/ |____/  |_| |_|_|\___|_|  \___|_|    \___/_/\_\_|___/\__(_)

    */

    2 filename sasautos "c:sasautos";

    3 check for existance

    EXISTS

    %put %sysfunc(ifc(%sysfunc(fileexist(c:/sasmacro/xpt2loc.sas))
     ,xpt2loc.sas exists
     ,xpt2loc.sas does not exist));

    xpt2loc.sas exists

    DOES NOT EXIST

    %put %sysfunc(ifc(%sysfunc(fileexist(c:/sasmacro/zzt2loc.sas))
     ,zzt2loc.sas exists
     ,zzt2loc.sas does not exist));

    zzt2loc.sas does not exist

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

Adding sas supplied macros with your autocall macros and querying available macros 
