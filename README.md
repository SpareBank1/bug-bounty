# bug bounty
Resources for SpareBank 1's private bug bounty program. See https://sparebank1.dev/bounty/.

## Burp scope file

Import [sb1-scope.json](sb1-scope.json) in Burp Suite in Target > Scope Options (cogwheel icon) > Load Options. Please make sure any active tasks adheres to the suite scope.

## Nettbank bedrift canary data

Examples of data belonging to another *nettbankavtale*, which you should not be able to access. Can be used to safely test access control, without requesting actual customer data.

Request missing canary data for your testcase at `bugbounty@sparebank1.no`.

### Agreement ID

`729239`

Used when selecting agreement:

```
PUT /smn/nettbank-bedrift/avtale/rest/avtale HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/avtale/velg-avtale
Connection: close
(...)

{"agreementId":"729239"}
```

### Account numbers
Used in multiple settings
```
42023152600
42123187622
42125381817
42125433884
42125434414
```

### *Mottakere*
https://www.sparebank1.no/smn/nettbank-bedrift/betaling/mottakere

IDs
```
94980894
76854011
94985990
```

### Transactions
https://www.sparebank1.no/smn/nettbank-bedrift/transaksjoner/kontobevegelser

transactionIds
```
821855043
714553598
592834770
``` 

Example requests
```
GET /smn/nettbank-bedrift/transaksjoner/rest/kontobevegelser/transaksjoner/42023152600/00000855043?accountedDate=29.08.2022 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/transaksjoner/kontobevegelser
(...)

```

```
GET /smn/nettbank-bedrift/transaksjoner/rest/kontobevegelser/transaksjoner/42023152600/33837830000?accountedDate=16.05.2022 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/transaksjoner/kontobevegelser
(...)

```

```
GET /smn/nettbank-bedrift/transaksjoner/rest/kontobevegelser/transaksjoner/42023152600/40104550000?accountedDate=10.01.2022 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/transaksjoner/kontobevegelser
(...)

```

### Files (*filarkiv*)

#### *Hent filer*
Existing IDs
```
652259732
31064737
1688958/560289746
```
Example requests
```
GET /smn/nettbank-bedrift/filer/rest/filer/652259732 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/filer/filarkiv
(...)

```

```
GET /smn/nettbank-bedrift/filer/rest/filer/31064737 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/filer/filarkiv
(...)

```

```
GET /smn/nettbank-bedrift/filer/rest/filer/1688958/560289746 HTTP/1.1
Host: www.sparebank1.no
Referer: https://www.sparebank1.no/smn/nettbank-bedrift/filer/filarkiv
(...)

```
#### *Filoppsett*
IDs
```
1712646
1525868
1714728
```
Note that `PUT /smn/nettbank-bedrift/filer/rest/filoppsett/1714728 HTTP/1.1` will return `HTTP/1.1 204 No Content`, but the *filoppsett* won't be modified.