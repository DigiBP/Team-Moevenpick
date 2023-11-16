# Team-Moevenpick

### Team-Member

|Name|Email|
|----------|---------------|
|Sascha Frossard|sascha.frossard@students.fhnw.ch|
|Selina Hodel|selina.hodel@students.fhnw.ch|
|Denis Moser|denis.moser@students.fhnw.ch|
|Marvin Marqua|marvin.marqua@students.fhnw.ch|

### Project Goal

1. Opimization of laboratory "Order to Report" process trough implementation of automated service Tasks, well defined process structure and separation of concerns.

2. Eliminating existing "dead ends" in the AS-IS processes two improve process quality.

## Process variables
| Variable          | Description                           | Data Type    |
|-------------------|---------------------------------------|--------------|
|orderId            | unique order id                       | string       |
|orderInternal      | true if order is internal             | boolean       |
|sampleId           | unique sample id                      | string        |
|sampleType         | Type of the received sample           | string        | ffpe, dna, bonemarrow
|orderFromComplete  |True if order form is complete         | boolean       |
|sampleAcceptanceOk | true if sample acceptance is fullfilled | boolean     |
|customerEmail      | email of the ordering client          | string        |
