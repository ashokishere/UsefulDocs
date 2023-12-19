SAST
SCA
DAST
IAST
IAC Security
API Security

Developer + Security + Operation
Shift Left Approach - Identiy security issue during Dev Life cycle
Starts from Code Implementation
Integrate Security in Operations( Scans after Deployments, Scan container Registry)

Development 
    Git Secrets
    Security Plugins (IDE, Intellj)
    Tufflehog

Security 
  SonarQube
  SAST Secuity Tools(Fortify, Veracode, blackDuck,Synk)
  DAST Tools( OWASP, ZAP, WebInspect, VeraCode, DAST, Acunetix)
  IAC( BrideCrewm Synk)
  Cotainer Security Tools( Auqa, Qulys,PrismaCloud)

Steps for pipeline

  1) Open Gitlab Trial
  2) Allow permission for github repository and import Repository
  3) master branch in needed as most of the tools use that.. Delete main branch
  4) change Defult brach to master(settings)
  5) Delete the main Branch
  6) open a account os SonarCloud
       Create Org and Org Key , Project Key and generate Token
  7) Update the pipeline .gitlab_ci.yml
     
  

