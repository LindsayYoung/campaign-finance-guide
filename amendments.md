# Understanding Schedule A

## Raw v. Processed
There are a few ways to access the data. If you are on the [FEC website for Schedule A](https://www.fec.gov/data/receipts/?data_type=processed&two_year_transaction_period=2020&min_date=01%2F01%2F2019&max_date=12%2F31%2F2020), You will notice that there is a data type toggle on the top. You can choose raw or processed. It defaults to processed data, this will take care of amendments, and will be data that is much easier to work with. The [raw data](https://www.fec.gov/data/receipts/?data_type=efiling) comes directly from efiling. This is the data feed you want if you are looking at filings that cam in within that day.

## Line numbers
Understanding line numbers it important if you want to work with the more granular data.

Working with individual records is tricky because there are a lot of codes that can apply to a record and the code can radical change the meaning of the record.

This is where you can really leverage the FEC website and API to really help you out. The `is_individual` flag can sort out the relevant line numbers for you so you can get all unique, individual line items.

Understanding individual records depend on understanding line numbers. You can see on the form below a check box in the upper right corner. That is where you can see the line numbers for the records on that form page.

<img src="/sched_A.png" alt="image of Schedule A form on Form 3, line numbers are check boxes in the top right and the information for a record is listed below" />

This example is from a [Form 3](https://www.fec.gov/documents/124/fecfrm3.pdf), this is a common form. It's used for House and Senate candidate committees. On of the best places to look for what line items items mean is looking at the [form instructions](https://www.fec.gov/help-candidates-and-committees/forms/) for the corresponding forms.

### Below are the line numbers for the Form 3, 3P and 3X

**Form 3** (House and Senate candidate committees):
- **11a** Contributions from individuals, partnerships and other persons who are not political committees.
- **11b** Contributions from political party committees
- **11c** Contributions from other political committees
- **11d** Contributions from the candidate
- **12** Transfers from other authorized committees of the same candidate
- **13a** Loans from the candidate
- **13b** All other loans
- **14** Offsets to operating expenditures such as: refunds, rebates, and
returns of deposits
- **15** Other receipts such as dividends and interest

**Form 3P** (Presidential candidate committees):
- **16** Federal funds
- **17a** Contributions from individuals other than political committees
- **17b** Contributions from political party committees
- **17c** Contributions from other political committees
- **17d** Contributions from the candidate
- **18** Transfers from other authorized committees of the same candidate
- **19a** Loans from the candidate
- **19b** All other loans
- **20a** Offsets to operating expenditures such as: refunds, rebates, and
returns of deposits
- **20b** Offsets to fundraising disbursements
- **20c** Offsets to legal and accounting disbursements
- **21** Other receipts such as dividends and interest

**Form 3X** (PACS and political parties)
- **11a** Contributions from individuals, partnerships and other persons who are not political committees.
- **11b** Contributions from political party committees
- **11c** Contributions from other political committees
- **11d** Contributions from the candidate
- **12** Transfers from other authorized committees of the same candidate
- **13** All loans
- **14** loan repayments
- **15** Offsets to operating expenditures such as: refunds, rebates, and returns of deposits
- **16** Refunds of contributions made to federal candidates and other political committees
- **17** Other receipts such as dividends and interest

Note that different line numbers can mean different things on different forms. There are more forms and more line numbers.

# Memos

In addition to the line numbers, you can also notice a "Memo item" check box. This has way more significance than first meets the eye. If the box is checked, that item is "memoed." Those items shouldn't be used for totals, they are generally, describing any pass-through entities. So, if I give money to a PAC and ask them to donate to a particular candidate, on the candidate's form you will see two transactions. One will be attributed to the individual and one will be "memoed" and attributed to the PAC I originally gave money too.

The text under the memo box can be present even if the box isn't checked. Sometimes, it says things that just, aren't helpful once you are looking at the data holistically. For example, "See below" is common but not optimized for data consumer.

## Amendments
When treasurers submit Amendments, they submit the entire form over again. You can see the full [amendment instructions for filers](https://www.fec.gov/help-candidates-and-committees/filing-amendments/) to get more details.

Also, keep in mind that the cycle to date totals don't always amended correctly, so use caution in using those.

## Other notes
If individuals give less than $200, committees are not required to report those donations.

If you are looking for those filing incorrectly (and I bet you have more sympathy for that now) you can also just look for committees who have gotten requests from the FEC clarifying their filings, by looking for [requests for additional information](https://www.fec.gov/data/filings/?data_type=processed&form_type=RFAI).
