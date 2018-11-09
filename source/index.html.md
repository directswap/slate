---
title: Direct Swap Deals and Terms API Reference

language_tabs:
  - shell
  - ruby
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Direct Swap API! You can use our API to access Deals and Terms
API endpoints, which you can use to populate and fetch information on Deals,
their associated Terms, and the status of those entities in our database.

We have language bindings in Shell, Ruby, and Python. You can view code examples
in the dark area to the right, and you can switch the programming language of
the examples with the tabs in the top right.

# Codes
The user should assume that where an ISO standard is available, this API uses 
that standard. For example, currency codes use the ISO 
standard: USD, RUB, CAD, etc.


# Authentication

> To authorize, use this code:

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('email','my-api-key')
```

```python
import directswap

api = directswap.authorize('email','my-api-key')
```

```shell
# With shell, you can pass the correct headers with each request
curl "api_endpoint"
  -H "X-User-Email: <your-email>" 
  -H "X-User-Token: <my-api-key>"
```

> Make sure to replace `my-api-key` with your API key.

Direct Swap uses API keys to allow access to the API. You can register a new
Direct Swap API key at our [developer portal](http://directswap.com/developers).

Direct Swap expects for the API key to be included in all API requests to the
server in a header that looks like the following:

```
X-User-Email: <your-email> 
X-User-Token: <my-api-key>
```

<aside class="notice">
You must replace <code>your-email</code> with your account email address.
You must replace <code>my-api-token</code> with your personal API key.
</aside>

# Deals

## Get All Deals

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('my-api-token')
api.deals.get
```

```python
import directswap

api = directswap.authorize('my-api-token')
api.deals.get()
```

```shell
curl "http://directswap.com/deals.json"
  -H "X-User-Email: <your-email>" 
  -H "X-User-Token: <my-api-key>"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "",
  },
  {
    "id": 2,
    "name": "",
  }
]
```

This endpoint retrieves all Deals.

### HTTP Request

`GET http://directswap.com/deals.json`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_terms | true | If set to true, the result will also include the term(s) on the deal.

## Get a Specific Deal

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('example@example.com','meowmeowmeow')
api.deals.get(2)
```

```python
import directswap

api = directswap.authorize('my@email.com','my-api-token')
api.deals.get(2)
```

```shell
curl "http://directswap.com/api/deals/2.json"
  -H "X-User-Email: <your-email>" 
  -H "X-User-Token: <my-api-key>"
```
> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "FOREX 123 Deal",
  
}
```

This endpoint retrieves a specific Deal.

### HTTP Request

`GET http://directswap.com/deals/<ID>.json`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the Deal to retrieve

## Create a New Deal

```ruby
require 'direct_swap'

api = DirectSwap::APIClient.authorize!('email@address.com','meowmeowmeow')
api.deals.create(deal_hash)
```

```shell
curl "http://directswap.com/api/deals.json"
  -H "X-User-Email: <your-email>" 
  -H "X-User-Token: <my-api-key>"
  --data 'param1=a&param2=b&param3=c'
```

```python
import directswap

api = directswap.authorize('my@email.com','my-api-token')
api.deals.create(deal_hash)
```

> The above command returns a JSON representation of the deal that was just
created, structured like this:

```json
{
  "id": 2,
  "name": "New FOREX Deal",
}
```

### HTTP Request

`POST http://directswap.com/deals.json`

### URL Parameters

Parameter | Description
--------- | -----------
state | The state of the deal. Deafults to "draft"
product_id | Direct Swap ProductID for the instrument you are offerring
instrument_id | Direct Swap InstrumentID for the instrument you are offering
alternate_id | Your internal reference number for the deal, e.g. "TMS_11235813",
description | Human Readable description of the deal, e.g. "10,000 mmBtu NATURAL GAS-HENRY HUB-NYMEX",
euce_reduces_risk | Affirmation that the deal qualifies for the End User Clearing Exception clause for Reducing Risk, defaults to false
euce_not_subject_to_position_limits | Affirmation that the deal qualifies for the End User Clearing Exception clause for Not Subject To Position Limits, defaults to false
euce_not_speculative | Affirmation that the deal qualifies for the End User Clearing Exception clause with respect to position limits, defaults to false
euce_not_hedging_another_swap |Affirmation that the deal qualifies for the End User Clearing Exception clause with respect to prohibition on hedging another swap, defaults to false
expires_at | Expiration date and time, e.g. Wed, 03 May 2017 00:00:00 UTC +00:00,
name | Name of the deal
sdr_reportable | Whether the deal is currently SDR Reportable, defaults to false




# Terms
## Get Specific Terms

### Parameters

The following attributes outline the possible set of parameters you will find on Deal Terms.

Parameter | Description | Commodity Swap | Commodity Cap/Floor | Currency Forward | Interest Rate Swap | Interest Rate Cap/Floor
--------- | ----------- |  ----------- |  ----------- |  ----------- |  ----------- |  ----------- |
id | Internal numeric ID of the terms| X | X | X | X | X |
entity_id | Internal entity ID of the entity proposing the terms| X | X | X | X | X |
deal_id | Internal numeric deal Identifier | X | X | X | X | X |
reporting_party_id | Entity ID of the party who will report to the SDR| X | X | X | X | X |
fixed_payer_id | Fixed Rate Payer | | | | | |
float_payer_id | Floating Rate Payer | | | | | |
created_at | Date of creation | | | | | |
updated_at | Last Updated Date | | | | | |
expiration | Date this offer expires | | | | | |
trade_date | Date of the trade| | | | | |
effective_date | Effective date of the deal | | | | | |
maturity_date | Maturity date of the instrument | | | | | |
cut_off_dates | A text list of dates: eg: '3/31, 6/30, 9/30, 12/31' | | | | | |
compounding | Counpounding Type (text) | | | | | |
calculation_agent_id | numeric ID of the Calculation Agent (one of the deal participants)| | | | | |
negative_interest_rate_method | or 'Not Applicable'| | | | | |
isda_definitions | | | | | | |
fixed_notional | | | | | | |
fixed_notional_currency | | | | | | |
fixed_payment_frequency |'Annual','Semi-Annual','Quarterly','Monthly','Daily' | | | | | |
fixed_accrual_basis | One of:  ['30/360', 'Actual/Actual', 'Actual/Actual (ICMA)', 'Actual/365', 'Actual/360', '1/1']| | | | | |
fixed_period_end_dates | | | | | | |
fixed_first_period_end_date | | | | | | |
fixed_period_business_day_convention |One of: 'Following','Preceding','No Adjustment','Modified Following' | | | | | |
fixed_period_business_day_center |One Of: ['New York','London','Frankfurt','Rome','Paris','Hong Kong','Tokyo','Singapore','Sydney']| | | | | |
fixed_settlement_dates | | | | | | |
fixed_first_settlement_date | | | | | | |
fixed_settlement_business_day_convention |One of: 'Following','Preceding','No Adjustment','Modified Following'| | | | | |
fixed_settlement_business_day_center |One Of: ['New York','London','Frankfurt','Rome','Paris','Hong Kong','Tokyo','Singapore','Sydney']| | | | | |
fixed_rate | | | | | | |
float_notional | | | | | | |
float_notional_currency | | | | | | |
float_payment_frequency |'Annual','Semi-Annual','Quarterly','Monthly','Daily'| | | | | |
float_accrual_basis | One of:  ['30/360', 'Actual/Actual', 'Actual/Actual (ICMA)', 'Actual/365', 'Actual/360', '1/1']| | | | | |
float_period_end_dates | | | | | | |
float_first_period_end_date | | | | | | |
float_period_business_day_convention |One of: 'Following','Preceding','No Adjustment','Modified Following'  | | | | | |
float_period_business_day_center |One Of: ['New York','London','Frankfurt','Rome','Paris','Hong Kong','Tokyo','Singapore','Sydney']| | | | | |
float_settlement_dates | | | | | | |
float_first_settlement_date | | | | | | |
float_settlement_business_day_convention |One of: 'Following','Preceding','No Adjustment','Modified Following'  | | | | | |
float_settlement_business_day_center |One Of: ['New York','London','Frankfurt','Rome','Paris','Hong Kong','Tokyo','Singapore','Sydney']| | | | | |
float_reset_dates | | | | | | |
float_first_reset_date | | | | | | |
float_reset_business_day_convention | | | | | | |
float_reset_business_day_center |One Of: ['New York','London','Frankfurt','Rome','Paris','Hong Kong','Tokyo','Singapore','Sydney']| | | | | |
float_spread | | | | | | |
float_first_period_rate | | | | | | |
float_index_maturity | | | | | | |
additional_terms | | | | | | |
fixed_notional_units | | | | | | |
fixed_notional_per_period | | | | | | |
specified_price | | | | | | |
averaging_method | | | | | | |
currency_conversion_provision | | | | | | |
delivery_date | | | | | | |
disruption_event | 'None','Price Source Disruption','Benchmark Obligation Default','Dual Exchange Rate','General Inconvertibility','General Nontransferability','General Inconvertibility/Nontransferability','Governmental Authority Default','Illiquidity','Material Change in Circumstance','Nationalization','Price Materiality','Specific Inconvertibility','Specific Nontransferability','Party Specific Event' | | X | | | |
disruption_fallback | 'Fallback Reference Price','Calculation Agent Determination of Settlement Rate','Assignment of Claim','Deliverable Substitute','Escrow Arrangement','Local Asset Substitute Gross','Local Asset Substitute Net','Local Currency Substitute','No Fault Determination','Non-Deliverable Substitute','Settlement Postponement'] | | | | | |
disruption_maximum_days | | | | | | |
electricity_settlement_days | Integer number of days | | | | | |
electricity_settlement_duration | | | | | | |
electricity_settlement_start | | | | | | |
electricity_settlement_stop | | | | | | |
side1_entity_id | | | | | | |
side1_buy_sell | | | | | | |
side1_notional | | | | | | |
side1_currency | | | | | | |
side2_entity_id | | | | | | |
side2_buy_sell | | | | | | |
side2_notional | | | | | | |
side2_currency | | | | | | |
settlement_type | | | | | | |
settlement_currency | | | | | | |
valuation_date | | | | | | |
disruption_details | | | | | | |
float_notional_per_period | | | | | | |
party_a_sec_5_a_v | | | | | | |
party_a_sec_5_a_vi | | | | | | |
party_a_sec_5_a_vii | | | | | | |
party_a_sec_5_b_v | | | | | | |
party_b_sec_5_a_v | | | | | | |
party_b_sec_5_a_vi | | | | | | |
party_b_sec_5_a_vii | | | | | | |
party_b_sec_5_b_v | | | | | | |
specified_transaction | | | | | | |
party_a_cross_default | | | | | | |
party_b_cross_default | | | | | | |
specified_indebtedness | | | | | | |
threshold_amount | | | | | | |
party_a_credit_event | | | | | | |
party_b_credit_event | | | | | | |
party_a_auto_early_term | | | | | | |
party_b_auto_early_term | | | | | | |
termination_currency | | | | | | |
party_a_additional_term | | | | | | |
party_b_additional_term | | | | | | |
party_a_sec_3_e | See legal language options below | | | | | |
party_a_sec_3_e_rep | If the party makes reps, freeform text here.  | | | | | |
party_b_sec_3_e | See legal language options below| | | | | |
party_b_sec_3_e_rep |If the party makes reps, freeform text here. | | | | | |
party_a_sec_3_f | | | | | | |
party_a_sec_3_f_rep | | | | | | |
party_a_sec_3_f_treaty | | | | | | |
party_a_sec_3_f_jurisdiction | | | | | | |
party_b_sec_3_f | | | | | | |
party_b_sec_3_f_rep | | | | | | |
party_b_sec_3_f_treaty | | | | | | |
party_b_sec_3_f_jurisdiction | | | | | | |
party_a_address | | | | | | |
party_a_attention | | | | | | |
party_a_telex | | | | | | |
party_a_answerback | | | | | | |
party_a_facsimile | | | | | | |
party_a_telephone | | | | | | |
party_a_email | | | | | | |
party_a_electronic_messaging | | | | | | |
party_a_specific_instructions | | | | | | |
party_b_address | | | | | | |
party_b_attention | | | | | | |
party_b_telex | | | | | | |
party_b_answerback | | | | | | |
party_b_facsimile | | | | | | |
party_b_telephone | | | | | | |
party_b_email | | | | | | |
party_b_electronic_messaging | | | | | | |
party_b_specific_instructions | | | | | | |
party_a_process_agent | | | | | | |
party_b_process_agent | | | | | | |
offices | | | | | | |
party_a_multiparty_branch | | | | | | |
party_a_multiparty_branch_offices | | | | | | |
party_b_multiparty_branch | | | | | | |
party_b_multiparty_branch_offices | | | | | | |
isda_ma_calculation_agent | | | | | | |
party_a_credit_support_documents | | | | | | |
party_b_credit_support_documents | | | | | | |
party_a_credit_support_provider | | | | | | |
party_b_credit_support_provider | | | | | | |
netting | | | | | | |
netting_details | | | | | | |
netting_effective_date | | | | | | |
affiliate | | | | | | |
party_a_absence_of_litigation | | | | | | |
party_b_absence_of_litigation | | | | | | |
no_agency | | | | | | |
additional_representations | | | | | | |
recording_conversations | | | | | | |
other_provisions | | | | | | |
party_a_additional_credit_support | | | | | | |
party_a_valuation_percentage | | | | | | |
party_b_additional_credit_support | | | | | | |
party_b_valuation_percentage | | | | | | |
party_a_independent_amount | | | | | | |
party_b_independent_amount | | | | | | |
party_a_posted_credit_support |Paragraph 6(c) [will not|will] apply | | | | | |
party_b_posted_credit_support |Paragraph 6(c) [will not|will] apply | | | | | |
base_currency | | | | | | |
valuation_date_city | | | | | | |
valuation_time_city | | | | | | |
existing_csa | | | | | | |
accepted_by_user_id | | | | | | |
state | | | | | | |
offered_to_entity_id | | | | | | |
in_response_to_offer_id | | | | | | |
governing_law | | | | | | |
settlement_day | | | | | | |
party_a_demands_and_notices | | | | | | |
party_b_demands_and_notices | | | | | | |
accepted_at | | | | | | |
created_by_user_id | | | | | | |
relationship_id | | | | | | |
common_pricing | | | | | | |
float_index_id | | | | | | |
disruption_fallback_price_id | | | | | | |
strike_price | | | | | | |
instrument_subtype | | | | | | |

Options for the legal language sections are listed below:

#### sec_3_e
  ['Does not make any representations',
   'It is not required by any applicable law, as modified by the practice ' \
   'of any relevant governmental revenue authority, of any Relevant ' \
   'Jurisdiction to make any deduction or withholding for or on account ' \
   'of any Tax from any payment (other than interest under Section 9(h) of ' \
   'this Agreement) to be made by it to the other party under this ' \
   'Agreement. In making this representation, it may rely on (i) the ' \
   'accuracy of any representations made by the other party pursuant to ' \
   'Section 3(f) of this Agreement, (ii) the satisfaction of the agreement ' \
   'contained in Section 4(a)(i) or 4(a)(iii) of this Agreement and the ' \
   'accuracy and effectiveness of any document provided by the other party ' \
   'pursuant to Section 4(a)(i) or 4(a)(iii) of this Agreement and (iii) ' \
   'the satisfaction of the agreement of the other party contained in ' \
   'Section 4(d) of this Agreement, except that it will not be a breach of ' \
   'this representation where reliance is placed on clause (ii) above and ' \
   'the other party does not deliver a form or document under Section ' \
   '4(a)(iii) by reason of material prejudice to its legal or commercial ' \
   'position.',
   'Makes the following representations:'

#### sec_3_f
  ['Does not make any representations',

   'It is fully eligible for the benefits of the “Business Profits” or ' \
   '“Industrial and Commercial Profits” provision, as the case may be, the ' \
   '“interest” provision or the “Other Income” provision, if any, of the ' \
   'Specified Treaty with respect to any payment described in such ' \
   'provisions and received or to be received by it in connection with ' \
   'this Agreement and no such payment is attributable to a trade or ' \
   'business carried on by it through a permanent establishment in the ' \
   'Specified Jurisdiction.',

   'Each payment received or to be received by it in connection with this ' \
   'Agreement will be effectively connected with its conduct of a trade or ' \
   'business in the Specified Jurisdiction.',

   'It is a “U.S. person” (as that term is used in section ' \
   '1.1441-4(a)(3)(ii) of United States Treasury Regulations) for United ' \
   'States federal income tax purposes.',

   'It is a “non-U.S. branch of a foreign person” (as that term is used ' \
   'in section 1.1441-4(a)(3)(ii) of United States Treasury Regulations) ' \
   'for United States federal income tax purposes.',

   'With respect to payments made to an address outside the United States ' \
   'or made by a transfer of funds to an account outside the United ' \
   'States, it is a “non-U.S. branch of a foreign person” (as that term is ' \
   'used in section 1.1441-4(a)(3)(ii) of United States Treasury ' \
   'Regulations) for United States federal income tax purposes.',

   'It is a “foreign person” (as that term is used in section ' \
   '1.6041-4(a)(4) of United States Treasury Regulations) for United ' \
   'States federal income tax purposes.',

   'Makes the following representations:']

#### recording_conversations
  ['Not applicable',
   'Each party (i) consents to the recording of telephone conversations ' \
   'between the trading, marketing and other relevant personnel of the ' \
   'parties in connection with this Agreement or any potential Transaction,' \
   ' (ii) agrees to obtain any necessary consent of, and give any ' \
   'necessary notice of such recording to, its relevant personnel and ' \
   '(iii) agrees, to the extent permitted by applicable law, that ' \
   'recordings may be submitted in evidence in any Proceedings.']

#### settlement_day
  ['One Local Business day immediately following such date',
   'Two Local Business days immediately following such date',
   'The same date']

#### additional_representations
  ['The Parties do not make any Additional Representations',
   'The Parties make the following Additional Representations:']

#### netting
  ['Will not apply',
   'Will apply to all Transactions',
   'Will apply to the following Transactions or groups of Transactions:']

#### multiparty_branch
  ['Party is not a Multibranch Party',
   'Party is a Multibranch Party and may enter into a Transaction through ' \
   'any of the following Offices:']

####



```json


```
## Add Terms to a deal

### For a Currency deal
Parameter | Description |
entity_id |
in_response_to_offer_id |
expiration | Offer Expiration |
side1_entity_id | Party 1
side1_buy_sell | Buy/Sell
side1_notional | Notional
side1_currency | Currency
side2_entity_id | Party 2
side2_buy_sell | Buy/Sell
side2_notional | Notional
side2_currency | Currency
maturity_date | Settlement Date
forward_rate | Forward Rate
settlement_type | Settlement Type
settlement_currency | Settlement Currency
valuation_date | Valuation Date
float_index_id | Settlement Rate Option
fixed_settlement_business_day_convention | Settlement Adjustment
fixed_settlement_business_day_center | Settlement Holiday Calendar
disruption_event | Market Disruption Events
disruption_fallback | Disruption Fallbacks
disruption_fallback_price_id | Fallback Reference Price
disruption_details | Disruption Fallback Details
isda_definitions | ISDA Definitions
calculation_agent | Calculation Agent
cut_off_dates | Cutoff Dates
addtional_terms | Additional Terms
reporting_party_id | Reporting Party

### For an Interest Rate  Deal
Parameter | Description |

### For a Commodities Deal
Parameter | Description |

# Products
## List All Products

### HTTP Request

`GET http://directswap.com/products.json`

> The above command returns a JSON representation of the product tree, 
structured like this:

```json
{ products:
    [
      {
        "id":1,
        "name":"Commodities",
        "parent_id":null,
        "created_at":"2017-05-01T16:45:22.166Z",
        "updated_at":"2017-05-01T16:45:22.166Z"
      },
      {
        "id":2,
        "name":"Agricultural",
        "parent_id":1,
        "created_at":"2017-05-01T16:45:22.167Z",
        "updated_at":"2017-05-01T16:45:22.167Z"
      },
      {
        "id":3,
        "name":"Dairy",
        "parent_id":2,
        "created_at":"2017-05-01T16:45:22.169Z",
        "updated_at":"2017-05-01T16:45:22.169Z"},{"id":4,
          "name":"Butter",
          "parent_id":3,
          "created_at":"2017-05-01T16:45:22.170Z",
          "updated_at":"2017-05-01T16:45:22.170Z"
      },
      {
        "id":5,
        "name":"Cheese",
        "parent_id":3,
        "created_at":"2017-05-01T16:45:22.170Z",
        "updated_at":"2017-05-01T16:45:22.170Z"
      }
    ]
  }
```

## Show a specific Product  

# Instruments
## List all Instruments


### HTTP Request

`GET http://directswap.com/instruments.json`

> The above command returns a JSON representation of the deal that was just
created, structured like this:

```json
{ instruments:
  [
    {
      "id":1,
      "name":"Swap",
      "created_at":"2017-05-01T16:45:22.148Z",
      "updated_at":"2017-05-01T16:45:22.148Z"},
    {
      "id":2,
      "name":"Cap/Floor",
      "created_at":"2017-05-01T16:45:22.150Z",
      "updated_at":"2017-05-01T16:45:22.150Z"
    },{
      "id":3,
      "name":"Forward",
      "created_at":"2017-05-01T16:45:22.151Z",
      "updated_at":"2017-05-01T16:45:22.151Z"
    },{
      "id":4,
      "name":"ISDA Master Agreement",
      "created_at":"2017-05-01T16:45:22.152Z",
      "updated_at":"2017-05-01T16:45:22.152Z"
    }
  ]
}
```

## Show a specific Instrument
