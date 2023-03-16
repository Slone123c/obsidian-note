

>%%
>```annotation-json
>{"created":"2023-01-13T05:59:42.156Z","text":"InnoDB uses primary key as clustered index. When we use it to search, it can save a lot of I/O operation.\nSecondary indexes refer to the primary keys that use to search for the row in the clustered index.","updated":"2023-01-13T05:59:42.156Z","document":{"title":"Designing Data-Intensive Applications","link":[{"href":"urn:x-pdf:f4030ab3256cbd6de727d8a4f1de8630"},{"href":"vault:/Reading/Designing Data-Intensive Applications.pdf"}],"documentFingerprint":"f4030ab3256cbd6de727d8a4f1de8630"},"uri":"vault:/Reading/Designing Data-Intensive Applications.pdf","target":[{"source":"vault:/Reading/Designing Data-Intensive Applications.pdf","selector":[{"type":"TextPositionSelector","start":231917,"end":232063},{"type":"TextQuoteSelector","exact":"he  primary  key  of  a  table  is  always  a  clustered  index,  andsecondary indexes refer to the primary key (rather than a heap file location)","prefix":"SQL’sInnoDB  storage  engine,  t","suffix":" [31]. InSQL Server, you can spe"}]}]}
>```
>%%
>*%%PREFIX%%SQL’sInnoDB  storage  engine,  t%%HIGHLIGHT%% ==he  primary  key  of  a  table  is  always  a  clustered  index,  andsecondary indexes refer to the primary key (rather than a heap file location)== %%POSTFIX%%[31]. InSQL Server, you can spe*
>%%LINK%%[[#^5j293x62hc4|show annotation]]
>%%COMMENT%%
>InnoDB uses primary key as clustered index. When we use it to search, it can save a lot of I/O operation.
>Secondary indexes refer to the primary keys that use to search for the row in the clustered index.
>%%TAGS%%
>##index
^5j293x62hc4


