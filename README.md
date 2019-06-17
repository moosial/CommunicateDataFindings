# Loan Data from Prosper
## by Christian Altmoos


### Data Set in general

This data set contains `113,937` loans with `81` variables on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, and many others. The dataset contains so-called listings which either have been transformed to a loan or not. Partially funded loans are possible as well. My main overall interest might be why and who is becoming a so-called Prosper borrower and furthermore what is mainly influencing the interest rate. Interesting woould be how the average Prosper rate is compared to the normal finacial market. 


### What is the structure of your dataset?
The overall structure can be found in this Google Docs [Spreadsheet](https://docs.google.com/spreadsheets/d/1gDyi_L4UvIrLTEC6Wri5nbaMmkGmLQBk-Yx3z0XDEtI/edit). Some further useful information I foud here:
* Prosper API Description [link](https://www.prosper.com/Downloads/Services/Documentation/ProsperDataExport_Details.html)
* Information on expected data types [link](https://bigml.com/user/mrlender/gallery/dataset/512e7695035d075e7c0000be)
* Expalanation Listing [link](https://www.prosper.com/invest/how-to-invest/search-listings/)
* Some articles to build up basic doamin knowledge:
    * Review Prosper [link1](https://www.bankrate.com/loans/personal-loans/reviews/prosper/)
    * Peer 2 Peer Lending vs. Bank Loan [link2](https://www.bankrate.com/loans/personal-loans/peer-to-peer-lending-vs-bank-loan/)
* Some fed data for interest rates [link](https://fred.stlouisfed.org/categories/101)

The data primarily consists out of 9 main categories, which obviously are merged in the given dataset.

* **Bid Object**: A Bid is created when a Lender wishes to lend money to a Borrower in response to a Listing the Borrower created to solicit Bids. Bids are created by specifying an Amount and a Minimum Rate in which the Lender wishes to receive should the Bid win the auction and become a Loan. The Minimum Rate remains private unless the Bid is Outbid by other Bids offering a lower Minimum Rate.

* **Category Object**: A Category is collection of Groups which share a common interest or affiliation. Categories are created by the Prosper Team. Group Leaders can associate their Group with one or more categories as they relate to their group. 

* **CreditProfile Object**: A CreditProfile is a timestamped set of extended credit information for a Member. Row level display and publication of CreditProfile is explicitly forbidden.

* **Group Object**: A Group is a collection of Members who share a common interest or affiliation. Groups are managed by Group Leaders who bring borrowers to Prosper, maintain the group's presence on the site, and collect and/or share Group Rewards. Borrowers who are members of a group often get better interest rates because Lenders tend to have more confidence in Borrowers that belong to trusted Groups. 

* **Listing Object**: A Listing is created by a Borrower to solicit bids by describing themselves and the reason they are looking to borrow money. If the Listing receives enough bids by Lenders to reach the Amount Requested then after the Listing period ends it will become a Loan. A Borrower may only have one active listing at a particular moment in time. 

* **Loan Object**: A Loan is created when a Borrower has received enough Bids to meet the full amount of money that the Borrower requested in their Listing. The Borrower must then make payments on the Loan to keep it's status current. 

* **Loan Performance Object**: A LoanPerformance is an event in a Loan History that causes a change in loan value. This table can be used to calculate roll rates. Row level display and publication of LoanPerformance is explicitly forbidden.

* **Marketplace Object**: The Marketplace is a collection of metrics and statistics about the Prosper Marketplace. These metrics are calculated daily. Historical metrics are provided as well. 

+ **Member Object**: A Member is a registered user of the Prosper Marketplace site. A Member may have one or multiple roles which determines which actions the Member is allowed to perform on the site. 



### What is/are the main feature(s) of interest in your dataset?

Based on  my high level questions I think these are the main attributes:

* **Who is using Prosper? (basically which individuals, which professions, which part of the country, financial situation)**
    * Occupation
    * EmploymentStatus
    * IsBorrowerHomeowner
    * BorrowerState
* **Why is Prosper used? (Is it related to rates, fees, or faster processing time)**
    * ListingCreationDate
    * LoanOriginationDate
    * ListingCategory
    * BorrowerAPR
    * BorrowerRate
    * ProsperRating 
    * Term 
    * LoanStatus
* **What is primarily influenicng the interest rate? (is it related to scoring, income and history)**
    * ProsperRating (Alpha)
    * ProsperScore
    * DebtToIncomeRatio
    * IncomeRange
    * MonthlyLoanPayment
    * Term 
    

### What features in the dataset do you think will help support your investigation into your feature(s) of interest?

I examined the stucture of the dataset utilizing the mentioned sources and categorized 3 main areas with the follwoing attributes. The main attributes are refrenced as **bold**. I assume the other attributes are helping to explain variations and patterns obeserved in the data. However they might be not taken into consideration, depending on the anylsis.

* **Key and Date Attributes**
    * **ListingNumber**: The number that uniquely identifies the listing to the public as displayed on the website.
    * **ListingCreationDate**: The date the listing was created.
    * **LoanOriginationDate**: The date the loan was originated.
    * MemberKey: The unique key that is associated with the borrower. This is the same identifier that is used in the API member object. 
* **Loan Attributes**
    * **ListingCategory**: The category of the listing that the borrower selected when posting their listing: 0 - Not Available, 1 - Debt Consolidation, 2 - Home Improvement, 3 - Business, 4 - Personal Loan, 5 - Student Use, 6 - Auto, 7- Other, 8 - Baby&Adoption, 9 - Boat, 10 - Cosmetic Procedure, 11 - Engagement Ring, 12 - Green Loans, 13 - Household Expenses, 14 - Large Purchases, 15 - Medical/Dental, 16 - Motorcycle, 17 - RV, 18 - Taxes, 19 - Vacation, 20 - Wedding Loans
    * **BorrowerAPR**: The Borrower's Annual Percentage Rate (APR) for the loan.
    * **BorrowerRate**: The Borrower's interest rate for this loan. 
    * **ProsperRating (numeric`)**: The  Prosper Rating assigned at the time the listing was created: 0 - N/A, 1 - HR, 2 - E, 3 - D, 4 - C, 5 - B, 6 - A, 7 - AA.  Applicable for loans originated after July 2009.
    * **ProsperRating (Alpha)**: The Prosper Rating assigned at the time the listing was created between AA - HR.  Applicable for loans originated after July 2009.
    * **ProsperScore**: A custom risk score built using historical Prosper data. The score ranges from 1-10, with 10 being the best, or lowest risk score.  Applicable for loans originated after July 2009.
    * **Term**: The length of the loan expressed in months.
    * **LoanStatus**: The current status of the loan: Cancelled,  Chargedoff, Completed, Current, Defaulted, FinalPaymentInProgress, PastDue. The PastDue status will be accompanied by a delinquency bucket.
    * ClosedDate: Closed date is applicable for Cancelled, Completed, Chargedoff and Defaulted loan statuses. 
    * **LoanOriginalAmount**: The origination amount of the loan.
    * **MonthlyLoanPayment**: The scheduled monthly loan payment.
    * PercentFunded: Percent the listing was funded.
    * InvestmentFromFriendsCount: Number of friends that made an investment in the loan.
    * InvestmentFromFriendsAmount: Dollar amount of investments that were made by friends.
    * Investors: The number of investors that funded the loan.
* **Loan - Borrower Attributes** 
    * **DebtToIncomeRatio**: The debt to income ratio of the borrower at the time the credit profile was pulled. This value is Null if the debt to income ratio is not available. This value is capped at 10.01 (any debt to income ratio larger than 1000% will be returned as 1001%).
    * **IncomeRange**: The income range of the borrower at the time the listing was created.
    * **Occupation**: The Occupation selected by the Borrower at the time they created the listing.
    * **EmploymentStatu**`: The employment status of the borrower at the time they posted the listing.
    * **EmploymentStatusDuration**: The length in months of the employment status at the time the listing was created.
    * **IsBorrowerHomeowner**: A Borrower will be classified as a homowner if they have a mortgage on their credit profile or provide documentation confirming they are a homeowner.
    * **BorrowerState**: The two letter abbreviation of the state of the address of the borrower at the time the Listing was created.
    * **EstimatedLoss**: Estimated loss is the estimated principal loss on charge-offs. Applicable for loans originated after July 2009.
    * **EstimatedReturn**: The estimated return assigned to the listing at the time it was created. Estimated return is the difference between the Estimated Effective Yield and the Estimated Loss Rate. Applicable for loans originated after July 2009.
    * CreditScoreRangeLower: The lower value representing the range of the borrower's credit score as provided by a consumer credit rating agency.
    * CreditScoreRangeUpper: The upper value representing the range of the borrower's credit score as provided by a consumer credit rating agency. 
    * CurrentCreditLines: Number of current credit lines at the time the credit profile was pulled.
    * OpenCreditLines: Number of open credit lines at the time the credit profile was pulled.
    * TotalCreditLinespast7years: Number of credit lines in the past seven years at the time the credit profile was pulled.
    * InquiriesLast6Months: Number of inquiries in the past six months at the time the credit profile was pulled.
    * CurrentDelinquencies: Number of accounts delinquent at the time the credit profile was pulled.
    * AmountDelinquent: Dollars delinquent at the time the credit profile was pulled.
    * DelinquenciesLast7Years: Number of delinquencies in the past 7 years at the time the credit profile was pulled.
    * RevolvingCreditBalance: Dollars of revolving credit at the time the credit profile was pulled.
    * BankcardUtilization: The percentage of available revolving credit that is utilized at the time the credit profile was pulled.
    * AvailableBankcardCredit: The total available credit via bank card at the time the credit profile was pulled.
    * IncomeVerifiable: The borrower indicated they have the required documentation to support their income.
    * StatedMonthlyIncome: The monthly income the borrower stated at the time the listing was created.
    * TotalProsperLoans: Number of Prosper loans the borrower at the time they created this listing. This value will be null if the borrower had no prior loans. 
    * TotalProsperPaymentsBilled: Number of on time payments the borrower made on Prosper loans at the time they created this listing. This value will be null if the borrower had no prior loans.
    * OnTimeProsperPayments: Number of on time payments the borrower had made on Prosper loans at the time they created this listing. This value will be null if the borrower has no prior loans.
    * ProsperPaymentsLessThanOneMonthLate: Number of payments the borrower made on Prosper loans that were less than one month late at the time they created this listing. This value will be null if the borrower had no prior loans. 
    * ProsperPaymentsOneMonthPlusLate: Number of payments the borrower made on Prosper loans that were greater than one month late at the time they created this listing. This value will be null if the borrower had no prior loans.
    * ProsperPrincipalBorrowed: Total principal borrowed on Prosper loans at the time the listing was created. This value will be null if the borrower had no prior loans.
    * ProsperPrincipalOutstanding: Principal outstanding on Prosper loans at the time the listing was created. This value will be null if the borrower had no prior loans.
    * ScorexChangeAtTimeOfListing: Borrower's credit score change at the time the credit profile was pulled. This will be the change relative to the borrower's last Prosper loan. This value will be null if the borrower had no prior loans.
    * Recommendations: Number of recommendations the borrower had at the time the listing was created.




### Univariate Exploration Summary

* `Cleaning General`:
The following attributes have being excluded: ListingKey, CreditGrade, CurrentlyInGroup, GroupKey, DateCreditPulled, FirstRecordedCreditLine, OpenRevolvingAccounts, OpenRevolvingMonthlyPayment, TotalInquiries, PublicRecordsLast10Years, PublicRecordsLast12Months, TotalTrades, ,TradesNeverDelinquent (percentage), TradesOpenedLast6Months, LoanKey, LoanCurrentDaysDelinquent, LoanFirstDefaultedCycleNumber, LoanMonthsSinceOrigination ,LoanNumber, LoanOriginationQuarter, LP_CustomerPayments, LP_CustomerPrincipalPayments, LP_InterestandFees, LP_ServiceFees, LP_CollectionFees, LP_GrossPrincipalLoss, LP_NetPrincipalLoss, LP_NonPrincipalRecoverypayments.

* `Prosper Rating`:
As we have 25% not populated becase the Prosper Rating started after July 2009 I thought maybe a simple rule (or even regression) for the derivation of the Prosper
rating based on the external one would be easy. But it is not as e.g. D is between 680 - 699 and E later down as well. So let's flag them as before_July09
and analyze keeping decide at th end to keep or to get rid of them.


* `BorrowerAPR`: There are a lot of values at the end in the bins of <font color='red'>0,35 - 0,36</font> (btw. which is more then 30%). However looking to the distribution I would say it can be considered as normal distributed.

* `DebtToIncomeRatio`: This isn't looking normal distributed at all. As it's a financial KPI and the original scale is pretty much right skewed, a log scale might better explain the distribution.

* `StatedMonthlyIncome`: The Q-Q Plot is not really underlining the normality. However the log transformed plot is really much more following a "bell-shape" then the original scale.

* `MonthlyLoan Payment`: Here are some values here which are extremly low below 10$ and tehy spread to different categories like completed etc. However out of those categories the proportion of 0 is very low. The log scale describes the data pretty normal.

* `EstimatedReturn`:The Estimated return is sometimes 0 or negative. Apart from that it looks pretty normal.

* `EstimatedLoss`: The data looks right-skewed, after teh log transform it look left-skewed, so I decide to saty with the original scale.


### Bivariate Exploration Summary

* `Summary Who is using Prosper`: 

    * It seems that the occupations and the status pretty clear shows that teh occupation groups "Others" 
    * "Profesional, "Executives" and "Computer Programmers" from Califirnia are most present.
    * There is a nearly equal split of Homeowners and Non-Homeowners, however the lesser the proportion of prosper user is the hisgher the homeowner propotion gets (with som eexceptions)
    * Most of the Prosper Users are "Employed (Fulltime)"
    * Most of the Prosper Users are using the loan for "Debt consolidation" 
    * The highest mean income do "Doctors" have 
    * The hishest mean DebtToIncomeRation do "Teacher's Aide" have.
    * The hightest mean loan amount do "Judges" have 
    * The most frequent Score is 4 along the "Others" and "Professional" group
    * The most frequent rating is C along the "Others" and "Professional" group

In general the occupation group "Other" is dominating the listings, whereas other occupations have a small proportion. This is a petty as it might be due to the fact that users have the possibility to choose from a ddlb the other category.

* `Summary: Why is Prosper used`?

    * Time2Money: Might be a reason,but fast is different, however the platform Prosper seems to accelarate with increasing listings count over time. There is a clear downward trend in Time2Money attribute, which might attract the borrowers.
    * BorrowerAPR over time: At the end of 2011 the rates have being considerable higher as before and it seems as this was the end of an upward trend, till the mid of 2014 it was constantly going down
    * BorrowerAPR by Occupation: Still not a bargain, the avg. Borrower APR is appr. 22%. Let's look if there is 

* `What is influencing the Rate`?

    * `BorrowerAPR vs. ProsperRating`: The distributions are nicely climbing with descresing the rating. Most of the distribution are bi- or multimodal. The spread in each categoy is as well large. On categories AA we find many outliers to the right. In A as well and C, D have outliers as well in both directions. E has outliers to the left. Again below as an example the density and viloin plot for "E"! HR has a relatively small IQR and many outliers to the left.
    * `BorrowerAPRvs. DebtToIncomeRatio`: As we know from the beginning the correlation coeff = 0,128, so we have a weak linear relation. Below 2 the rates are going the full range we need to zoom in a bit. One thing which is looking strange is the nearly vertical line between 0,35 and appr. 0,37 along all D2IR.The majority of the values is concentrated between 0,1 and 0,4 and  0,10 to 0,25. We can see a slight upward trend in the concentrated area, but the rate alos must be influenced by something else.
    * `BorrowerAPR vs Term`: We know from the Univariate Analysis that 12 month term are very seldom bit they have a lower rates as a starting point of their distributions. So 36 seems to be multimodal and 60 right skewed. Still all 3 terms give overlall a wide range of of rates. In 36 we see the 3rd modality which is looking similar to the concentration we saw in teh DTIR between 0,35 and 0,37 let's look closer. The Medians are close to each other, the range for 60 is smaller. So this can might explain the peak line we saw in the D2IR I was mentionong before, however either it is a combination of attributes or it is another attribute which is primarily deriving the rate.
    * `ProsperScore`: We can see that the medians of the rates are increasing by decreasing the score. However 2 things are here interesting. 
        * The scores 7 - 3 are relatively wide IQRs and no (nearly) outliers. 
        * Whereas 10 to 8  and 2 to 1 are  have many outliers to the right and to the left.
        * The groups 11 and 1 are relatively small. So there is still soethong else which controls the rates.
    * `BorrowerRate vs. IncomeVerifiable`: The appr. 10% not having a verified income do get higher rates. So having all documetns ready helps as well here.
    * `BorrowerAPR vs. IsBorrowerHomeowner`: To own a house definity helps. We can clearly see that the median rate is lower for houseowners. 
    * `BorrowerAPR vs. StatedMonthyIncome`: We can see on the log scale that the most frequent area is 1900 and above 20000 (I mean it's monthly income). However the range of APR is still going from 5 - above 40%. Having a lot of money/month is not a indecation to get better rates. We see that the fit isn't really good but the it empahsizes a bit the less income the higher the rate. In the heatmap we see a that the range goes from 0,1 to 0,4 through all income levels.
    * `BorrowerAPR vs. IncomeRange`:  This makes it really visible the platform Prosper is used by well earning lenders, the spike between 0.3 and 0.4. Having a higher income definitly helps to get teh best rates, however there i smuch variance in the ditributions. The proportion of below 25k and even unemployed is very small. 
    * `BorrowerAPR vs. MonthlyPayment`: The monthly payment seems to have a limit at appr. 1000$ this is where below most of the rates are concentrated a slight trend can be seen that lower rates are drawn by higher monthly payments.
    * `BorrowerAPR vs. LoanAmount`: The higher the loan the spread of rates decreases.
    * `BorrowerAPR vs. EstimatedLos`: The smaller the loss thw smaller the APR. We can speak here about astrong negative realtionship....so what about the estimated Return?
    * `Estimated Return`: Surprisingly the Return is as well in negative relationship to the APR. Why is that? It's the way how it is calculated. The estimated yield which is the difference between the estimated yield and the loss.


### Multivariate Exploration Summary


* The 90 days moving average indicates that there is a nearly constant around appr. 11days
* The Time2Money by the top 10 occupations do not differ a lot compared to the overall average. As well as in comparison to the mean Time to Money (appr. 11days) and the mean Loan Amount(appr. 9300$) over all occupations. This means the speed of the listing process is not significantly differing. If the Time to Money attribute is a factor for Borrowers to use Prosper can't be finally proofed as we would need to compare it with e.g. processing times of traditional banks. 
* Loan Amount vs. the BorrowerAPR by Occupation is pretty much intresting. The mean APR and Loan is pretty much close to each other, however Compter Programmers get the best rates on average, 19,10%. Administrative Assistants get the worst rates, 25,59. Interesting is the fact that loan amounts e.g. 20k seem to have primarily rates better than the average of the respective occupation group. See above the red arrow annotations in the other group. However if the rates are so good to attract the borrowers would need to be analyzed with other data, e.g. data from bankloans for similar purposes and runtimes. For me the rates seem to be far high expecially today (and compared to Germany). 
* HighRisk borrowers seem to borrow less money
* The better the rating the better the lower (better) the APR and the Estimated Loss will be 
* With increasing  income the range of loan amount increases 
* Not employed boorowers aren't existent
* The higher the income the higher the lower the rates
* If the income can be proofed makes a significant difference
* Only a small proportion of the loans were given w/o income validation
* Having real estate property helps to get better rates 
* The longer the term the higher the loan amount
* The rates seem to be for 12 and 60 month terms slighty beter than for 36 month terms
* Prosper Rating is a mighty evaluation metric. We can clearly see that the distribtion of APR is getting worse from HR to AA. Futhermore we can see that the rates are increasing with higher indebtedness (at least slightly) and descreasing Prosper Rating. Same for the estimated loss it gets slightly higher higher by increasing indebtedness, but much more by the assignment to the respective Prosper Rating. 
* The time to Money moving average showed 11 dayss on a total level, the unsmoothed key-figure was much more volatile. 
* There is a phenonemen that the "nice" loan amounts like 15k, 20k, 25k are getting better rates inside the top10 occupations. That could be analyzed further.