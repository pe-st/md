# Tandem / HPE Nonstop

## pathcom

```
>pathcom $gp00
=delete sc

=reset server
=set server processtype oss
=...
=add server sc

=start sc
=freeze sc
=stop sc
=stop sc
=thaw sc
=start sc

=alter server sc, param LOG-FLAG "0"
=alter server sc, ARGLIST &
-DLOG_LEVEL=info,&
-DFO_ENV=dev,&
-XX:+PrintGCDetails,-XX:+PrintGCDateStamps,&
-XX:+UseGCLogFileRotation,-XX:NumberOfGCLogFiles=10,-XX:GCLogFileSize=20M,&
-Xloggc:/fo/dev/log/sc_gc.log,&
com.path.to.MyClass


=(Ctrl-Y)
```
