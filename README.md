# TechNotes

1) Adding hours to a date
${time:millisecondsToDateTime(time:dateTimeToMilliseconds(time:now()) - (4 * 3600 * 1000))}
2) https://streamsets.com/documentation/datacollector/latest/help/datacollector/UserGuide/Pipeline_Configuration/Expressions.html#concept_vqr_sqc_wr
3) To remove all special characters from a field name
https://ask.streamsets.com/question/79/how-to-remove-special-characters-from-a-field-name/

4) KAFKA_37 - Cannot parse record from message 'dev.Attendance.raw::2::29810': com.streamsets.pipeline.lib.parser.DataParserException: 
DATA_PARSER_02 - Parser error: 'org.apache.avro.AvroRuntimeException: Malformed data. Length is negative: -40'

In Kafka producer, untick the include schema box in configuration 

5) KAFKA_37 - Cannot parse record from message 'dev.Attendance.raw::0::29607': com.streamsets.pipeline.lib.parser.DataParserException: 
DATA_PARSER_02 - Parser error: 'org.apache.avro.AvroRuntimeException: Malformed data. Length is negative: -62'

In Kafka producer, change the format to avro 

6) To change date format to string and use in other JDBCs 
${time:extractStringFromDate(record:value('/dtAttendance'),'yyyy-MM-dd') }

7) com.google.common.util.concurrent.UncheckedExecutionException: com.streamsets.pipeline.api.base.OnRecordErrorException: 
JDBC_35 - Parsed record had 6 columns but SDC expected 7.

If the look up gives same column name twice, then this error will be given.

For Eg: select distinct ats.txtEmpNo, ats.dtAttendance, 
al.dtFromDate, al.dtToDate, al.numPercent, imp.txtProjectClassIndicator, ste.dtFromDate

8) Dataflow Triggers Overview

https://docs.streamsets.com/portal/#datacollector/3.5.1/help/datacollector/UserGuide/Event_Handling/EventFramework-Title.html#concept_d1q_xl4_lx
