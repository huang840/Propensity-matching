# Propensity-matching

/*some costs are read in character, have to use substr to select data length*/
   data all    ;
       %let _EFIERR_ = 0; /* set the ERROR detection macro variable */
     *infile 'C:\Users\Swordfish\Google Drive\Purdue\Daily Med\DAILYMED_PRIMARY_OUTCOMES.csv' delimiter = ','
  MISSOVER DSD lrecl=32767 firstobs=2 ;
 infile 'C:\Users\huang840\Documents\DAILYMED_PRIMARY_OUTCOMES.csv' delimiter = ','
  MISSOVER DSD lrecl=32767 firstobs=2 ;
          informat Disposition $12. ;           informat Dailymedenrolled best32. ;          informat RID best32. ;
          informat Index_Date DATE8. ;          informat Inptvisitpre best32. ;          informat los_pre best32. ;
          informat Inptvisit_AHRQ_pre best32. ;          informat Inptvisitpost best32. ;          informat Inptvisitpost_CENSORED best32. ;
          informat IPPOST_180 best32. ;          informat IPPOST_180_CENSORED best32. ;          informat Inpt_timetoadmit best32. ;
          informat Los_post best32. ;          informat Inpt_AHRQ_post best32. ;          informat Inpt_AHRQ_CENSORED best32. ;
          informat Inpt_AHRQ_180 best32. ;          informat Inpt_AHRQ_180_CENSORED best32. ;          informat Inpt_AHRQ_timetoadmit best32. ;
          informat Otptvisits_pre best32. ;          informat Otptvisit_post best32. ;          informat N_er_pre best32. ;
          informat N_er_AHRQ_pre best32. ;          informat N_er_post best32. ;          informat n_er_post_CENSOR best32. ;
          informat N_ER_POST_180 best32. ;          informat n_er_post_180_CENSORED best32. ;          informat ER_timetoadmit best32. ;
          informat N_er_AHRQ_post best32. ;          informat ER_AHRQ_post_CENSOR best32. ;          informat n_er_AHRQ_180 best32. ;
          informat ER_AHRQ_POST_180_censored best32. ;          informat COST_OP_PRE $12. ;          informat COST_ER_PRE $12. ;
          informat COST_IP_PRE $12. ;          informat OP_COST_POST $12. ;          informat COST_ER_POST comma32. ;
          informat COST_IP_POST $12. ;          informat nursing_home_visits best32. ;          informat CHF1 best32. ;
          informat VALVE1 best32. ;          informat PULMCIRC1 best32. ;          informat PERIVASC1 best32. ;
          informat PARA1 best32. ;          informat HTN_C1 best32. ;          informat NEURO1 best32. ;
          informat CHRNLUNG1 best32. ;          informat DM1 best32. ;          informat DMCX1 best32. ;
          informat HYPOTHY1 best32. ;          informat RENLFAIL1 best32. ;          informat LIVER1 best32. ;
          informat ULCER1 best32. ;          informat AIDS1 best32. ;          informat LYMPH1 best32. ;
          informat METS1 best32. ;          informat TUMOR1 best32. ;          informat ARTH1 best32. ;
          informat COAG1 best32. ;          informat OBESE1 best32. ;          informat WGHTLOSS1 best32. ;
          informat LYTES1 best32. ;          informat BLDLOSS1 best32. ;          informat ANEMDEF1 best32. ;
          informat ALCOHOL1 best32. ;          informat DRUG1 best32. ;          informat PSYCH1 best32. ;
          informat DEPRESS1 best32. ;          informat Totalscore best32. ;          informat marital best32. ;
          informat ETHNICITY best32. ;          informat MEMBER_COUNTY best32. ;          informat age best32. ;
          informat gender best32. ;          informat PHONE_CALL_GROUP $1. ;          informat healthplan best32. ;
          informat strat_level best32. ;          informat dailymedcalls best32. ;          informat total_num_mo best32. ;
          informat number_mos_cont best32. ;          informat total_num_fills best32. ;          informat keep best32. ;
          informat N_rx_pre best32. ;          informat N_rx_post best32. ;          informat Cost_pharm_pre best32. ;
          informat Cost_pharm_post best32. ;

          format Disposition $12. ;          format Dailymedenrolled best12. ;          format RID best12. ;
         format Index_Date DATE8. ;        format Inptvisitpre best12. ;         format los_pre best12. ;
         format Inptvisit_AHRQ_pre best12. ;         format Inptvisitpost best12. ;         format Inptvisitpost_CENSORED best12. ;
         format IPPOST_180 best12. ;         format IPPOST_180_CENSORED best12. ;         format Inpt_timetoadmit best12. ;
         format Los_post best12. ;         format Inpt_AHRQ_post best12. ;         format Inpt_AHRQ_CENSORED best12. ;
         format Inpt_AHRQ_180 best12. ;         format Inpt_AHRQ_180_CENSORED best12. ;         format Inpt_AHRQ_timetoadmit best12. ;
         format Otptvisits_pre best12. ;         format Otptvisit_post best12. ;
         format N_er_pre best12. ;         format N_er_AHRQ_pre best12. ;         format N_er_post best12. ;
         format n_er_post_CENSOR best12. ;         format N_ER_POST_180 best12. ;         format n_er_post_180_CENSORED best12. ;
         format ER_timetoadmit best12. ;         format N_er_AHRQ_post best12. ;         format ER_AHRQ_post_CENSOR best12. ;
         format n_er_AHRQ_180 best12. ;         format ER_AHRQ_POST_180_censored best12. ;         format COST_OP_PRE $12. ;
         format COST_ER_PRE $12. ;         format COST_IP_PRE $12. ;         format OP_COST_POST $12. ;
         format COST_ER_POST comma12. ;         format COST_IP_POST $12. ;         format nursing_home_visits best12. ;
         format CHF1 best12. ;         format VALVE1 best12. ;         format PULMCIRC1 best12. ;
         format PERIVASC1 best12. ;        format PARA1 best12. ;         format HTN_C1 best12. ;
         format NEURO1 best12. ;         format CHRNLUNG1 best12. ;         format DM1 best12. ;
         format DMCX1 best12. ;         format HYPOTHY1 best12. ;         format RENLFAIL1 best12. ;
         format LIVER1 best12. ;         format ULCER1 best12. ;         format AIDS1 best12. ;
         format LYMPH1 best12. ;         format METS1 best12. ;         format TUMOR1 best12. ;
         format ARTH1 best12. ;         format COAG1 best12. ;         format OBESE1 best12. ;
         format WGHTLOSS1 best12. ;         format LYTES1 best12. ;         format BLDLOSS1 best12. ;
        format ANEMDEF1 best12. ;         format ALCOHOL1 best12. ;         format DRUG1 best12. ;
         format PSYCH1 best12. ;         format DEPRESS1 best12. ;         format Totalscore best12. ;
         format marital best12. ;         format ETHNICITY best12. ;         format MEMBER_COUNTY best12. ;
         format age best12. ;         format gender best12. ;         format PHONE_CALL_GROUP $1. ;
         format healthplan best12. ;         format strat_level best12. ;         format dailymedcalls best12. ;
         format total_num_mo best12. ;         format number_mos_cont best12. ;         format total_num_fills best12. ;
         format keep best12. ;         format N_rx_pre best12. ;         format N_rx_post best12. ;
         format Cost_pharm_pre best12. ;         format Cost_pharm_post best12. ;
      input
                  Disposition $                  Dailymedenrolled                  RID
                  Index_Date                  Inptvisitpre                  los_pre
                  Inptvisit_AHRQ_pre                  Inptvisitpost                  Inptvisitpost_CENSORED
                  IPPOST_180                  IPPOST_180_CENSORED                  Inpt_timetoadmit
                  Los_post                  Inpt_AHRQ_post                  Inpt_AHRQ_CENSORED
                  Inpt_AHRQ_180                  Inpt_AHRQ_180_CENSORED                  Inpt_AHRQ_timetoadmit
                  Otptvisits_pre                  Otptvisit_post                  N_er_pre                  N_er_AHRQ_pre
                  N_er_post                  n_er_post_CENSOR                  N_ER_POST_180                  n_er_post_180_CENSORED
                  ER_timetoadmit                  N_er_AHRQ_post                  ER_AHRQ_post_CENSOR                  n_er_AHRQ_180
                  ER_AHRQ_POST_180_censored                  COST_OP_PRE $                  COST_ER_PRE $                  COST_IP_PRE $
                  OP_COST_POST $                  COST_ER_POST                  COST_IP_POST $                  nursing_home_visits
                  CHF1                  VALVE1                  PULMCIRC1                  PERIVASC1                  PARA1
                  HTN_C1                  NEURO1                  CHRNLUNG1                  DM1                  DMCX1
                  HYPOTHY1                  RENLFAIL1                  LIVER1                  ULCER1                  AIDS1
                  LYMPH1                  METS1                  TUMOR1                  ARTH1                  COAG1
                  OBESE1                  WGHTLOSS1                  LYTES1                  BLDLOSS1                  ANEMDEF1
                  ALCOHOL1                  DRUG1                  PSYCH1                  DEPRESS1                  Totalscore
                  marital                  ETHNICITY                  MEMBER_COUNTY                  age                  gender
                  PHONE_CALL_GROUP $                  healthplan                  strat_level                  dailymedcalls
                  total_num_mo                  number_mos_cont                  total_num_fills                  keep                  N_rx_pre
                  N_rx_post                  Cost_pharm_pre                  Cost_pharm_post
      ;
if PULMCIRC1=1 or CHRNLUNG1=1 then  Asthma=1;
else if  PSYCH1=1 or DEPRESS1=1 then Psydepress=1;
else if DM1=1 or DMCX1=1  then Diabetes=1;
   array dis{3} Asthma Psydepress Diabetes;
   do i = 1 to 3;
     if dis{i} =. then dis{i} =0;
   end;
   drop i;

      if _ERROR_ then call symputx('_EFIERR_',1);  /* set ERROR detection macro variable */
      run;

/**/

/*Asthma Psydepress Diabetes*/

/*create column for PSM
Covariates: age, sex, race, preindex ED visits, preindex hospitalization(s), total number of Elixhauser comorbidities
preindex medical and pharmacy costs, number of unique prescriptions medications 
taken during the 12-month preindex period*/
data psm;
set all (rename=(OP_COST_POST=COST_OP_POST));
COSTOPPRE=compress(COST_OP_PRE,'$,');
COSTERPRE=compress(COST_ER_PRE,'$,');
COSTIPPRE=compress(COST_IP_PRE,'$,');
COSTOPPOST=compress(COST_OP_POST,'$,');
COSTERPOST=compress(COST_ER_POST,'$,');
COSTIPPOST=compress(COST_IP_POST,'$,');
totalcost=sum(Cost_pharm_pre, COSTOPPRE, COSTERPRE, COSTIPPRE);
totalcostafter=sum(Cost_pharm_post, COSTOPPOST, COSTERPOST, COSTIPPOST);
run;
/*log transformation cost data*/

* First let's look at the scatterplot to see the relationship;

title1 'Original Variables';
symbol1 v=circle i=rl;

proc reg data=psm noprint;;
	model totalcost=age gender ethnicity CHF1
VALVE1 PERIVASC1 PARA1 HTN_C1 NEURO1 HYPOTHY1
RENLFAIL1 LIVER1 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1
ARTH1 COAG1 OBESE1 WGHTLOSS1 LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes
 
  ;
	output out = notrans_pre r = resid_pre;

	model totalcostafter=age gender ethnicity CHF1
VALVE1 PERIVASC1 PARA1 HTN_C1 NEURO1 HYPOTHY1
RENLFAIL1 LIVER1 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1
ARTH1 COAG1 OBESE1 WGHTLOSS1 LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes
 ;
	output out = notrans_post r = resid_post;
run;

symbol1 i=sm70;
/*
proc univariate data=notrans_pre noprint;; 
	var resid_pre; qqplot/normal (L=1 mu = est sigma=est);
proc univariate data=notrans_post noprint;; 
	var resid_post; qqplot/normal (L=1 mu = est sigma=est);
run;
*/
data psm_1;
set psm (rename=(totalcost=totalcost_1 totalcostafter=totalcostafter_1 
COSTIPPRE=COSTIPPRE_1 COSTIPPOST=COSTIPPOST_1 COSTOPPRE=COSTOPPRE_1
COSTOPPOST=COSTOPPOST_1 COSTERPRE=COSTERPRE_1 COSTERPOST=COSTERPOST_1
Cost_pharm_pre=Cost_pharm_pre_1 Cost_pharm_post=Cost_pharm_post_1));
totalcost=totalcost_1+1;
totalcostafter=totalcostafter_1+1;
COSTIPPRE=COSTIPPRE_1+1;
COSTIPPOST=COSTIPPOST_1+1;
COSTOPPRE=COSTOPPRE_1+1;
COSTOPPOST=COSTOPPOST_1+1;
COSTERPRE=COSTERPRE_1+1;
COSTERPOST=COSTERPOST_1+1;
Cost_pharm_pre=Cost_pharm_pre_1+1;
Cost_pharm_post=Cost_pharm_post_1+1;
run;


/*suggest 0.25 but hard to explain so we decide  to use log*/
data psm_2;
set psm_1;
logtotalcost=log(totalcost);
logtotalcostafter=log(totalcostafter);
logCOSTIPPRE=log(COSTIPPRE);
logCOSTIPPOST=log(COSTIPPOST);
logCOSTOPPRE=log(COSTOPPRE);
logCOSTOPPOST=log(COSTOPPOST);
logCOSTERPRE=log(COSTERPRE);
logCOSTERPOST=log(COSTERPOST);
logCost_pharm_pre=log(Cost_pharm_pre);
logCost_pharm_post=log(Cost_pharm_post);
run;

/* to see qq plot after transformation*/
proc reg data=psm_2 noprint;
	model logtotalcost=age gender ethnicity CHF1
VALVE1 PERIVASC1 PARA1 HTN_C1 NEURO1 HYPOTHY1
RENLFAIL1 LIVER1 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1
ARTH1 COAG1 OBESE1 WGHTLOSS1 LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes 
  ;
	output out = notrans_pre r = resid_pre;

	model logtotalcostafter=age gender ethnicity CHF1
VALVE1 PERIVASC1 PARA1 HTN_C1 NEURO1 HYPOTHY1
RENLFAIL1 LIVER1 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1
ARTH1 COAG1 OBESE1 WGHTLOSS1 LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes
 ;
	output out = notrans_post r = resid_post;
run;

symbol1 i=sm70;


proc sort data=psm; by Disposition;
run;
/*****original population ***************************/
OPTIONS MCOMPILENOTE=ALL;
options symbolgen;
%macro mtests (aa=psm);
proc means data=&aa.; var age N_er_pre Inptvisitpre totalcost N_rx_pre; by Disposition;run;
proc ttest cochran ci=equal data=&aa.; var age ; class disposition;
proc ttest cochran ci=equal data=&aa.; var N_er_pre ; class disposition;
proc ttest cochran ci=equal data=&aa.; var Inptvisitpre; class disposition;
proc ttest cochran ci=equal data=&aa.; var totalcost; class disposition;
proc ttest cochran ci=equal data=&aa.; var N_rx_pre; class disposition;run;

proc freq data=&aa.;
tables gender*disposition ethnicity*disposition CHF1*disposition 
VALVE1*disposition PULMCIRC1*disposition PERIVASC1*disposition 
PARA1*disposition HTN_C1*disposition NEURO1*disposition 
CHRNLUNG1*disposition DM1*disposition DMCX1*disposition 
HYPOTHY1*disposition RENLFAIL1*disposition LIVER1*disposition 
 ULCER1*disposition AIDS1*disposition LYMPH1*disposition 
METS1*disposition TUMOR1*disposition ARTH1*disposition 
COAG1*disposition OBESE1*disposition WGHTLOSS1*disposition 
LYTES1*disposition BLDLOSS1*disposition ANEMDEF1*disposition 
ALCOHOL1*disposition DRUG1*disposition PSYCH1*disposition 
DEPRESS1*disposition Asthma*disposition Psydepress*disposition
Diabetes*disposition/chisq ;
run;
%mend mtests;
/*%mtests()*/



proc logistic data=psm_2;
model Disposition=age gender N_rx_pre N_er_pre 
Inptvisitpre ethnicity CHF1
VALVE1 PERIVASC1 PARA1 HTN_C1 NEURO1 HYPOTHY1
RENLFAIL1 LIVER1 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1
ARTH1 COAG1 OBESE1 WGHTLOSS1 LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes 
totalcost / selection=stepwise risklimits lackfit rsquare parmlabel; output out=psset 
pred=prob ;
run;



data psset1;
set psset;
hid=1;
if disposition="Not_Enrolled" then disposition1=0;
else disposition1=1;
run;



OPTIONS MCOMPILENOTE=ALL;
options symbolgen;
/* Include the matching macro code */
*%include 'C:\Users\Swordfish\Dropbox\Purdue\Zillich\work beggings\meetings\MacroOneToManyMatch.txt';
%include 'C:\Users\huang840\Dropbox\Purdue\Zillich\work beggings\meetings\MacroOneToManyMatch.txt';

/*matches_1 is the final results*/
/* Call Macro and Perform 1:1 Match */
%OneToManyMTCH(work,psset1,disposition1,hid,RID,Matches_1,1);
/* Call Macro and Perform 1:2 Match */
%OneToManyMTCH(work,psset1,disposition1,hid,RID,Matches_2,2);
/* Call Macro and Perform 1:3 Match */
%OneToManyMTCH(work,psset1,disposition1,hid,RID,Matches_3,3);
/* Call Macro and Perform 1:4 Match */
%OneToManyMTCH(work,psset1,disposition1,hid,RID,Matches_4,4);



/*after matching results*/
data After;
set Matches_2;
COSTOPPRE=compress(COST_OP_PRE,'$,');
COSTERPRE=compress(COST_ER_PRE,'$,');
COSTIPPRE=compress(COST_IP_PRE,'$,');
totalcost=sum(Cost_pharm_pre, COSTOPPRE, COSTOPPRE, COSTIPPRE);
proc sort; by disposition;
run;
/*%mtests(aa=After)*/




/*start to draw the differences after and before matching*/
/*start to draw the differences after and before matching*/
/*have to be in the same file, so combime two files*/

data Matches_2_1 ;
set Matches_2;
match='after';
keep disposition disposition1 prob match totalcost totalcostafter COSTIPPRE
COSTIPPOST COSTOPPRE COSTOPPOST COSTERPRE COSTERPOST Cost_pharm_pre Cost_pharm_post 
totalscore
logtotalcost logtotalcostafter logCOSTIPPRE
logCOSTIPPOST logCOSTOPPRE logCOSTOPPOST logCOSTERPRE logCOSTERPOST logCost_pharm_pre logCost_pharm_post 
;
data Psset1_1;
set Psset1;
match='before';
keep disposition disposition1 prob match totalcost totalcostafter COSTIPPRE
COSTIPPOST COSTOPPRE COSTOPPOST COSTERPRE COSTERPOST Cost_pharm_pre Cost_pharm_post
totalscore
logtotalcost logtotalcostafter logCOSTIPPRE
logCOSTIPPOST logCOSTOPPRE logCOSTOPPOST logCOSTERPRE logCOSTERPOST logCost_pharm_pre logCost_pharm_post 
;
data comb;
length match $8;
set Matches_2_1 Psset1_1;
;run;

data comb_1;
set comb;
if match='before' then before=prob;
else if match='after' then after=prob;
proc sort data=comb_1; by disposition;run;
/*There are a lot of costs equal zero*/

/*some costs are zero => 2*2 table to examine the zero and non-zero distribution*/
data zeroc;
set Matches_2;
if logtotalcost=0 then totalcostzero="=0";
else if logtotalcost not eq 0 then totalcostzero=">0";
if logtotalcostafter=0 then totalcostafterzero="=0";
else if logtotalcostafter not eq 0 then totalcostafterzero=">0";

if logCOSTIPPRE=0 then COSTIPPREzero="=0";
else if logCOSTIPPRE not eq 0 then COSTIPPREzero=">0";
if logCOSTIPPOST=0 then COSTIPPOSTzero="=0";
else if logCOSTIPPOST not eq 0 then COSTIPPOSTzero=">0";

if logCOSTOPPRE=0 then COSTOPPREzero="=0";
else if logCOSTOPPRE not eq 0 then COSTOPPREzero=">0";
if logCOSTOPPOST=0 then COSTOPPOSTzero="=0";
else if logCOSTOPPOST not eq 0 then COSTOPPOSTzero=">0";

if logCOSTERPRE=0 then COSTERPREzero="=0";
else if logCOSTERPRE not eq 0 then COSTERPREzero=">0";
if logCOSTERPOST=0 then COSTERPOSTzero="=0";
else if logCOSTERPOST not eq 0 then COSTERPOSTzero=">0";

if logCost_pharm_pre=0 then Cost_pharm_prezero="=0";
else if logCost_pharm_pre not eq 0 then Cost_pharm_prezero=">0";
if logCost_pharm_post=0 then Cost_pharm_postzero="=0";
else if logCost_pharm_post not eq 0 then Cost_pharm_postzero=">0";
run;

proc freq data=zeroc;
table totalcostzero*totalcostafterzero COSTIPPREzero*COSTIPPOSTzero
COSTOPPREzero*COSTOPPOSTzero COSTERPREzero*COSTERPOSTzero
Cost_pharm_prezero*Cost_pharm_postzero/chisq ; run;
proc freq data=zeroc;
table totalcostzero*totalcostafterzero COSTIPPREzero*COSTIPPOSTzero
COSTOPPREzero*COSTOPPOSTzero COSTERPREzero*COSTERPOSTzero
Cost_pharm_prezero*Cost_pharm_postzero/fisher ; run;




/*end - some costs are zero => 2*2 table to examine the zero and non-zero distribution*/


/*create per patient cost */
proc sql;
create table Matches_2_2 as
select disposition,
count (disposition) as num_p,
/*sum (totalcost) as allcpre,
sum (totalcostafter)as allcpost,
sum (COSTIPPRE)as ipcpe,
sum (COSTIPPOST)as ipcpost,
sum (COSTOPPRE) as opcpre,
sum (COSTOPPOST) as opcpost,
sum (COSTERPRE) as ercpre,
sum (COSTERPOST) as ercpost,
sum (Cost_pharm_pre) as pharmcpre,
sum (Cost_pharm_post) as pharmcpost,
sum (totalscore) as elix,*/

avg (totalcost) as avgallcpre,
avg (totalcostafter)as avgallcpost,
avg (COSTIPPRE)as avgipcpre,
avg (COSTIPPOST)as avgipcpost,
avg (COSTOPPRE) as avgopcpre,
avg (COSTOPPOST) as avgopcpost,
avg (COSTERPRE) as avgercpre,
avg (COSTERPOST) as avgercpost,
avg (Cost_pharm_pre) as avgpharmcpre,
avg (Cost_pharm_post) as avgpharmcpost,
avg (totalscore) as avgelix

from Matches_2_1
group by disposition;
quit;

data alldisease;
set Matches_2_2;
disease='all';
run;
/*create per patient cost ended */


title 'Before and After';
proc sgplot data=comb; by match;
where prob<0.3;
histogram prob /binwidth=0.005 group=disposition transparency=0.5;
  density prob   / group=disposition legendlabel='invovled' lineattrs=(pattern=solid);
  keylegend / location=inside position=topright across=1;
  *xaxis display=(nolabel);  run;

title 'Before and After - Cost Histogram ';
proc sgplot data=comb; by match;
where totalcost<50000;
histogram totalcost /binwidth=1000 group=disposition transparency=0.5;
  density totalcost    / group=disposition legendlabel='invovled' lineattrs=(pattern=solid);
  keylegend / location=inside position=topright across=1;
  *xaxis display=(nolabel);  run;


  /*bias reduction calculation*/

proc sort data=psset1; by disposition1;
proc means data=psset1 noprint;by disposition1; output out=meanss; run;
proc transpose data=meanss out=meanss_1; run;
/*prematch-continuous variable*/
data meanss_2;
set meanss_1 (rename=(COL4=mean_0 COL5=std_0 COL9=mean_1 COL10=std_1) );
diff=mean_1-mean_0;
sqrr=sqrt((std_0*std_0+std_1*std_1)/2);
stdiff=diff/sqrr;
run;


/*aftermatch-continuous variable*/
proc sort data=Matches_2; by disposition1;
proc means data=Matches_2 noprint;by disposition1; output out=m_meanss; run;
proc transpose data=m_meanss out=m_meanss_1; run;
data m_meanss_2;
set m_meanss_1 (rename=(COL4=mean_0 COL5=std_0 COL9=mean_1 COL10=std_1) );
diff=mean_1-mean_0;
sqrr=sqrt((std_0*std_0+std_1*std_1)/2);
m_stdiff=diff/sqrr;
run;

proc sql;
create table bias as
select A.*, B.m_stdiff
from meanss_2 A left join m_meanss_2 B on A._NAME_=B._NAME_;
quit;

data bias_1;
set bias;
reduction=((m_stdiff-stdiff)/stdiff)*100;
keep _NAME_ reduction stdiff m_stdiff;
run;
/*
proc export data=bias_1
outfile='C:\Users\Swordfish\Dropbox\Purdue\Zillich\work beggings\meetings\bias reduction_category.xlsx'
dbms=excel replace;
sheet='continuous';
run;
*/

/*prematch-categorical variable
 1 and 0*/
%macro chi (aa=CHF1);
proc freq data=psset1 noprint; by disposition1 ; tables &aa.*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data &aa.;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;
%mend chi;
proc sort data=psset1; by disposition1 ; 
proc freq data=psset1 noprint; by disposition1 ; tables CHF1*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data CHF1;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;

%chi()%chi(aa=VALVE1)
%chi(aa=PERIVASC1)%chi(aa=PARA1)%chi(aa=HTN_C1)
%chi(aa=NEURO1)
%chi(aa=HYPOTHY1)%chi(aa=RENLFAIL1)%chi(aa=LIVER1)%chi(aa=ULCER1)
%chi(aa=AIDS1)%chi(aa=LYMPH1)%chi(aa=METS1)%chi(aa=TUMOR1)
%chi(aa=ARTH1)%chi(aa=COAG1)%chi(aa=OBESE1)%chi(aa=WGHTLOSS1)
%chi(aa=LYTES1)%chi(aa=BLDLOSS1)%chi(aa=ANEMDEF1)%chi(aa=ALCOHOL1)
%chi(aa=DRUG1)
%chi(aa=Asthma) %chi(aa=Psydepress) %chi(aa=Diabetes)

/*deal with gender*/
proc freq data=psset1 noprint; by disposition1 ; tables gender*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data gender (rename=(COL2=COL1 COL4=COL3));
set psset_t; 
p1=COL1/100;p2=COL3/100;
drop COL1 COL3;
run;



data all_chi;
set  gender CHF1 VALVE1 PERIVASC1
PARA1 HTN_C1 NEURO1
HYPOTHY1 RENLFAIL1 LIVER1 
 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1 ARTH1
COAG1 OBESE1 WGHTLOSS1
LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 Asthma Psydepress Diabetes; run;

/*pre_match standarized difference*/
data chi_diff;
set all_chi;
p1p2=abs(p1-p2);
abss=abs((p1*(1-p1)+p2*(1-p2))/2);
sqrrp1p2=sqrt(abss);
diff=p1p2/sqrrp1p2;
seq+1;
run;

/*after match-categorical variable
 1 and 0*/
%macro chi (aa=CHF1);
proc freq data=Matches_2 noprint; by disposition1 ; tables &aa.*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data &aa.;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;
%mend chi;
%chi()%chi(aa=VALVE1)
%chi(aa=PULMCIRC1)%chi(aa=PERIVASC1)%chi(aa=PARA1)%chi(aa=HTN_C1)
%chi(aa=NEURO1)%chi(aa=CHRNLUNG1)%chi(aa=DM1)%chi(aa=DMCX1)
%chi(aa=HYPOTHY1)%chi(aa=RENLFAIL1)%chi(aa=LIVER1)%chi(aa=ULCER1)
%chi(aa=AIDS1)%chi(aa=LYMPH1)%chi(aa=METS1)%chi(aa=TUMOR1)
%chi(aa=ARTH1)%chi(aa=COAG1)%chi(aa=OBESE1)%chi(aa=WGHTLOSS1)
%chi(aa=LYTES1)%chi(aa=BLDLOSS1)%chi(aa=ANEMDEF1)%chi(aa=ALCOHOL1)
%chi(aa=DRUG1)%chi(aa=PSYCH1) %chi(aa=DEPRESS1)
/*deal with gender*/
proc freq data=Matches_2 noprint; by disposition1 ; tables gender*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data gender (rename=(COL2=COL1 COL4=COL3));
set psset_t; 
p1=COL1/100;p2=COL3/100;
drop COL1 COL3;
run;
data all_chi_after;
set  gender CHF1 VALVE1 PULMCIRC1 PERIVASC1
PARA1 HTN_C1 NEURO1 CHRNLUNG1 DM1 DMCX1
HYPOTHY1 RENLFAIL1 LIVER1 
 ULCER1 AIDS1 LYMPH1 METS1 TUMOR1 ARTH1
COAG1 OBESE1 WGHTLOSS1
LYTES1 BLDLOSS1 ANEMDEF1
ALCOHOL1 DRUG1 PSYCH1 DEPRESS1; run;

/*after_match standarized difference*/
data chi_diff_after;
set all_chi_after;
p1p2=abs(p1-p2);
abss=abs((p1*(1-p1)+p2*(1-p2))/2);
sqrrp1p2=sqrt(abss);
diff_after=p1p2/sqrrp1p2;
seq+1;run;

/*combine two files to calculate reduction*/
proc sql;
create table chi_diff_compare as
select a.*, b.diff_after 
from Chi_diff A left join Chi_diff_after B on
A.seq=B.seq; quit;

data chi_diff_compare_1;
set chi_diff_compare;
reduction=((diff_after-diff)/diff)*100;
run;
/*
proc export data=chi_diff_compare_1
outfile='C:\Users\huang840\Dropbox\Purdue\Zillich\work beggings\meetings\bias reduction_category.xlsx'
dbms=excel replace;
sheet='categorical';
run;
*/



/*trying to fix BLDLOSS1
not in the excel output problem*/

%macro chi (aa=CHF1);
proc freq data=psset1 noprint; by disposition1 ; tables &aa.*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data &aa.;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;
%mend chi;
proc sort data=psset1; by disposition1 ; 
proc freq data=psset1 noprint; by disposition1 ; tables CHF1*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data CHF1;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;

%chi(aa=BLDLOSS1)

data all_chi;
set BLDLOSS1; run;

data chi_diff;
set all_chi;
p1p2=abs(p1-p2);
abss=abs((p1*(1-p1)+p2*(1-p2))/2);
sqrrp1p2=sqrt(abss);
diff=p1p2/sqrrp1p2;
seq+1;
run;


%macro chi (aa=CHF1);
proc freq data=Matches_4 noprint; by disposition1 ; tables &aa.*disposition  / out=perce; run;
proc transpose data=perce out=psset_t;run;
data &aa.;
set psset_t ; 
p1=COL2/100;p2=COL4/100;
drop COL2 COL4;
run;
%mend chi;
%chi(aa=BLDLOSS1)

data all_chi_after;
set  BLDLOSS1; run;


data chi_diff_after;
set all_chi_after;
p1p2=abs(p1-p2);
abss=abs((p1*(1-p1)+p2*(1-p2))/2);
sqrrp1p2=sqrt(abss);
diff_after=p1p2/sqrrp1p2;
seq+1;run;


proc sql;
create table chi_diff_compare as
select a.*, b.diff_after 
from Chi_diff A left join Chi_diff_after B on
A.seq=B.seq; quit;

data chi_diff_compare_1;
set chi_diff_compare;
reduction=((diff_after-diff)/diff)*100;
run;

/*fix end fix end fix end fix end fix end fix end*/




/*DIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDID*/

/* UNADJUSTED REPEATED MEASURES ANOVA */



/*******ttteeesssttt*************************************************/

/*pre-post manupuation*/

data forplot_b;
set Matches_2 (rename=(logCOSTIPPRE=logcost_ip logCOSTOPPRE=logcost_op
logCOSTERPRE=logcost_er logCost_pharm_pre=logCost_pharm));
keep RID disposition logtotalcost time logcost_ip logcost_op logcost_er logCost_pharm; 
time=0;
data forplot_a;
set Matches_2 (keep= RID disposition logtotalcostafter logCOSTIPPOST logCOSTOPPOST
logCOSTERPOST logCost_pharm_post);
rename logtotalcostafter=logtotalcost
logCOSTIPPOST=logcost_ip logCOSTOPPOST=logcost_op
logCOSTERPOST=logcost_er logCost_pharm_post=logCost_pharm;
time=1;
data forplot;
set forplot_a forplot_b;
run;


/*UNADJUSTED REPEATED MEASURES LINEAR REGRESSION*/
PROC MIXED DATA = forplot;
CLASS disposition time;
MODEL logtotalcost=time|disposition / SOLUTION;
LSMEANS time|disposition / DIFF;
ESTIMATE 'D-I-D' disposition*time 1 -1 -1 1;
/*RANDOM INT/SUBJECT=STUDY_ID TYPE=UN ;*/
/*FORMAT disposition  disposition_GROUP. time PREPOST.;*/
TITLE2 "";
TITLE3 "UNADJUSTED: INCLUDING LEAST-SQUARES MEANS ESTIMATES";
RUN;

/*********ttteeesssttt
success! for the following 
code we will use it*********************************************/








/*****************************************************
*******************************************************
**************long data manupulation and use
in order to create a table***************************************/
%macro didd(bb=logtotalcost, cc=total cost);
PROC MIXED DATA = forplot;
CLASS disposition time;
MODEL &bb.=time|disposition / SOLUTION;
LSMEANS time|disposition / DIFF;
ESTIMATE 'D-I-D' disposition*time 1 -1 -1 1;
/*RANDOM INT/SUBJECT=STUDY_ID TYPE=UN ;*/
/*FORMAT disposition  disposition_GROUP. time PREPOST.;*/
TITLE1 "&cc. total cost DID";
TITLE2 "UNADJUSTED: INCLUDING LEAST-SQUARES MEANS ESTIMATES";
RUN; 
%mend didd;
%didd()
%didd(bb=logcost_ip, cc=Inpatient Cost)
%didd(bb=logcost_op, cc=Outpatient Cost)
%didd(bb=logcost_er, cc=Emergency Cost)
%didd(bb=logCost_pharm, cc=Pharmacy Cost)



/*****************************************************
*******************************************************
****************************************************/


/*********short data ******/
/*DID-total cost*/
PROC GLM DATA = Matches_2;
CLASS disposition1;
MODEL logtotalcost logtotalcostafter =disposition1 ;
REPEATED TIME 2 / PRINTE MEAN;
LSMEANS disposition1 ;
LSMEANS disposition1 / DIFF ;
TITLE2 "Repeated Measures Anova for Pre/Post Total cost By MTM Group";
QUIT;
/*DID-inpatient cost*/

PROC GLM DATA = Matches_2;
CLASS disposition1;
MODEL logCOSTIPPRE logCOSTIPPOST =disposition1 ;
REPEATED TIME 2 / PRINTE MEAN;
LSMEANS disposition1 ;
LSMEANS disposition1 / DIFF ;
TITLE2 "Repeated Measures Anova for Pre/Post Inpatients By MTM Group";
QUIT;

/*DID-outpatient cost*/

PROC GLM DATA = Matches_2;
CLASS disposition1;
MODEL logCOSTOPPRE logCOSTOPPOST =disposition1 ;
REPEATED TIME 2 / PRINTE MEAN;
LSMEANS disposition1 ;
LSMEANS disposition1 / DIFF ;
TITLE2 "Repeated Measures Anova for Pre/Post Outpatients By MTM Group";
QUIT;

/*DID-emergency cost*/

PROC GLM DATA = Matches_2;
CLASS disposition1;
MODEL logCOSTERPRE logCOSTERPOST =disposition1 ;
REPEATED TIME 2 / PRINTE MEAN;
LSMEANS disposition1 ;
LSMEANS disposition1 / DIFF ;
TITLE2 "Repeated Measures Anova for Pre/Post Emergency Patient By MTM Group";
QUIT;

/*DID-pharmacy cost*/

PROC GLM DATA = Matches_2;
CLASS disposition1;
MODEL logCost_pharm_pre logCost_pharm_post =disposition1 ;
REPEATED TIME 2 / PRINTE MEAN;
LSMEANS disposition1 ;
LSMEANS disposition1 / DIFF ;
TITLE2 "Repeated Measures Anova for Pre/Post Pharmacy Cost By MTM Group";
QUIT;




/* 
pre-post data: This turns on the graph editing function:
ods listing sge=on;*/
%macro forplot(aa=logtotalcost) ;
   proc glimmix data=forplot;
      class disposition time;
      model &aa.= time disposition time*disposition;
      lsmeans time*disposition / plot=mean(sliceby=disposition join);
   run;
%mend forplot;
%forplot()
%forplot(aa=logcost_ip) %forplot(aa=logcost_op) 
%forplot(aa=logcost_er) %forplot(aa=logCost_pharm) 

/*DIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDIDDID*/
