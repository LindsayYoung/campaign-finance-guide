# Campaign Finance Data Primer

This is meant to help people with an interest in data that are new to campaign finance. Campaign finance can be great data to work with, but it can get a bit complicated and there are a few pitfalls that are easy to fall into if you are navigating the data for the first time. This primer highlights good places to start, and points to other data you can use to dive deeper.

## Where does the data come from?

The [Federal Election Commission](https://www.fec.gov/) (FEC) is the source for campaign finance information for federal elections. Federal elections include Presidential, Senate and House races. State and local campaign finance data varies widely and isn't aggregated at the federal level. This explainer is about federal campaign finance.

All the data comes from committees who file forms with the FEC. Across those forms, similar types of data are grouped into schedules, such as receipts or disbursements.

## Committees

All campaign finance information is associated with different categories of committees. These are the groups or individuals that raise or spend money to support or oppose a candidate. Different types of committees abide by different rules file, different forms, and are subject to different [contribution limits](https://www.fec.gov/help-candidates-and-committees/candidate-taking-receipts/contribution-limits/).

### Common committee types:

- **House** , **Senate** , and **Presidential** committees are candidate committees. These are the most straightforward. They support a candidate.

- **Party** committees are also straightforward. They are committees of political parties.

- Political Action Committees ( **PAC** s) are the committees that currently raise the most money overall.  These are groups that raise and spend money in support or opposition of a candidate or candidates. They also make donations to candidates or other PACs. There are many different kinds of PACs.

- **Independent expenditure** committees come in a few types. An **Independent expenditor** is a person or group that spends over $250 on independent expenditures. **Independent expenditure only committees,** commonly known as Super PACs, don't have contributions limits but are not allowed to coordinate with candidate committees.

There are additional committee types. Here are [all committee types](https://www.fec.gov/campaign-finance-data/committee-type-code-descriptions/), with brief explanations. There are also different designations and organization types that apply to committees. You can see a list of these in the [FEC's API documentation for committees](https://api.open.fec.gov/developers/#/committee/get_committees_).

## Totals for committee and candidates

The FEC is a good place to compare [Presidential](https://www.fec.gov/data/candidates/president/?election_year=2020&amp;cycle=2020&amp;election_full=true), [Senate](https://www.fec.gov/data/candidates/senate/?election_year=2020&amp;cycle=2020&amp;election_full=true&amp;is_active_candidate=true), and [House](https://www.fec.gov/data/candidates/house/?election_year=2020&amp;election_full=True&amp;is_active_candidate=true) candidates' totals. Candidates can have more than one committee going, so those pages of the FEC's website will make sure you are looking at the whole picture.

If you are looking at a specific race, you will probably be interested in more than just the candidate's committees. You can [look up a race](https://www.fec.gov/data/elections/?state=&amp;cycle=2020&amp;election_full=true) to see Candidate committees, outside spenders, and other sources of money involved in the race.

## Granular data

The data from the forms that committees submit to the FEC is organized into schedules. Schedules are especially important if you want itemized data, such as contributor information. Schedules are aggregated, and totals for the schedules are reported on the corresponding form. Each of the schedules below comes from multiple forms.

### [**Receipts**](https://www.fec.gov/data/browse-data/?tab=raising) - Money coming into committees.

**Schedule A** - Covers all the itemized receipts that committees list on their forms. (Giving to a campaign isn't the legal definition of a donation. But these contributions are commonly called donations.) This is a large data set to work with. The data can also be a bit tricky.

The main thing to note is that if a donation is given to a committee with the purpose of giving it to another committee (usually a candidate committee), **that contribution will show up twice:** once in the records for each committee. If you are trying to aggregate donations, you can avoid that problem in the [FEC site](https://www.fec.gov/data/receipts/?data_type=processed&amp;two_year_transaction_period=2020), by clicking " From unique individuals only". If you're using the FEC API, you can do the same thing by setting the "is\_individual" parameter to true.

Keep in mind that the same name can appear differently across the data, sometimes nicknames are used or people's names are misspelled. People's locations can change as people move. Also more than one person can have the same name. If you are looking at contributors you will need to do some research to make sure your totals are right.

Independent expenditure only committees don't report their contributions, so you will not find entries for them on Schedule A. Groups that don't report donors are often referred to as "dark money" groups.

### [**Disbursements**](https://www.fec.gov/data/browse-data/?tab=spending) - what campaigns are spending (other than independent expenditures).

**Schedule B** - Covers all the itemized disbursements that committees report to the FEC, which you can use to see what committees are spending their money on. This is the data that you want to look at if you want to find "scam PACs", where the recipient of the funds is channeling money to themselves or their businesses without making many expenditures on supporting or opposing candidates.

[**Independent Expenditures**](https://www.fec.gov/data/independent-expenditures/?data_type=processed&amp;is_notice=false) - communications that support or oppose candidates that are not made in cooperation with a candidate. These can come from any type of committee that can make independent expenditures.

**Schedule E** - Breakdown of independent expenditures as reported to the FEC. Not all groups report where the money comes from, but you can still see where the money goes to.

There are also more kinds of data you may want to look at. [**Party coordinated expenditures**](https://www.fec.gov/data/party-coordinated-expenditures/) are money spent by a party in coordination with a candidate. [**Electioneering communications**](https://www.fec.gov/data/electioneering-communications/) are a type of communication close to an election that refers to a candidate but doesn't explicitly "support or oppose" that candidate. [**Communication costs**](https://www.fec.gov/data/communication-costs/) are are from corporation, labor organization, trade association, or membership organizations who advocate in support or opposition of a candidate to personnel, members, or stockholders.

## Forms

Since all of the data originates from forms that committees submit to the FEC, it helps to have a sense of what the forms are. When the data gets confusing, it can be helpful to read the instructions for the corresponding form.

### Common forms:

- **Statement of Organization** [Form 1](https://www.fec.gov/resources/cms-content/documents/fecfrm1i.pdf) - Register new candidate committees.

- **Statement of Candidacy** [Form 2](https://www.fec.gov/resources/cms-content/documents/fecfrm2i.pdf) - Register candidates for House, Senate and President.

- **Report of Receipts and Disbursements** Forms [3](https://www.fec.gov/resources/cms-content/documents/fecfrm3i.pdf), [3P](https://www.fec.gov/resources/cms-content/documents/fecfrm3pi.pdf), [3X](https://www.fec.gov/resources/cms-content/documents/fecfrm3xi.pdf), and [3L](https://www.fec.gov/resources/cms-content/documents/fecfrm3li.pdf) - These forms are where most of the information about money raised and spent comes from. These are filed by committees, and the timing of these forms can be semi-annual, quarterly, monthly, or 12 days before any election and 30 days after a general election. Here is a [calendar](https://www.fec.gov/calendar/?calendar_category_id=25&amp;calendar_category_id=26&amp;calendar_category_id=27) with these deadlines. Which form is filed depends on what kind of committee it is.

- **Report of Independent Expenditures Made and Contributions Received** [Form 5](https://www.fec.gov/resources/cms-content/documents/fecfrm5i.pdf) - Independent expenditures by and contributions to groups that support or oppose candidates, without coordination with that candidate.

There are several other forms. Here you can find [all forms](https://www.fec.gov/help-candidates-and-committees/forms/) and their instructions for reference. As you do more advanced searches, it is helpful to know what the purpose of each form is, so that you can narrow your search results down to the ones you want.

## What kind of data do you want?

There are great resources from the FEC and from the outside. Once you have an understanding of the data and where it comes from, you will want to choose where to get your data based on what kind of question you are trying to answer and how you want to interact with your data.

### _I want to know what candidates are raising or spending the most in a race:_

The FEC is a good place to compare [Presidential](https://www.fec.gov/data/candidates/president/?election_year=2020&amp;cycle=2020&amp;election_full=true), [Senate](https://www.fec.gov/data/candidates/senate/?election_year=2020&amp;cycle=2020&amp;election_full=true&amp;is_active_candidate=true), and [House](https://www.fec.gov/data/candidates/house/?election_year=2020&amp;election_full=True&amp;is_active_candidate=true) candidates totals.

### _I want the aggregate totals of contributions made by each contributor:_

Working with the schedules directly can be pretty labor intensive, so you might want to start with [OpenSecret's donor lookup](https://www.opensecrets.org/donor-lookup). They have already put in the effort to clean the data and consolidate contributions by each unique contributor, so you don't have to.

 ### _I want to see campaign finance data in the context of other information about races:_

[ProPublica](https://projects.propublica.org/electionbot/) provides campaign finance data alongside Google searches, polling, Facebook ads, news articles, and statements.

### _I want detailed data where I can look at trends over time:_

If you really want all of the data, you can download the [bulk datasets](https://www.fec.gov/data/browse-data/?tab=bulk-data) in csv and ".fec" format from the FEC. Summary files are good for looking at high level totals for committees and candidates. Contributions and expenditures are good for granular data, like who is contributing or what committees are spending their money on.

### _I want to access granular data through an API:_

 FEC offers an [API](https://api.open.fec.gov/developers/) with documentation. ProPublica also runs a campaign finance [API](https://projects.propublica.org/api-docs/campaign-finance/).

### _I want email updates for specific filings:_

[ProPublica](https://projects.propublica.org/electionbot/) provides a service that can send you email updates for specific races you want to follow.

### _I want real time updates as filings come in:_

Electronic filings are reported in real time, so you can see [receipts](https://www.fec.gov/data/receipts/?data_type=efiling), [filings](https://www.fec.gov/data/filings/?data_type=efiling), etc. on the FEC website. You can also use the "[efiling](https://api.open.fec.gov/developers/#/efiling)" endpoints on the FEC API as well as the [schedule a](https://api.open.fec.gov/developers/#/receipts/get_schedules_schedule_a_efile_)and [schedule b](https://api.open.fec.gov/developers/#/disbursements/get_schedules_schedule_b_efile_) efiling endpoints.

### _I want information on state elections:_

State elections are important too! The National Institute on Money in Politics operates [followthemoney.org](https://www.followthemoney.org/) where you can find state and some local campaign finance information. Otherwise, you have to find the information across various states in various formats.

### _I want information on election results:_

[Open elections](http://openelections.net/) normalizes election data from across the country in to a usable

### _I want information about legislators:_

The [@unitedstates GitHub](https://github.com/unitedstates) organization has a wide range of information about Congress.

Happy searching!
