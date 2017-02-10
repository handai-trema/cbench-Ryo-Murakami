##解答
まず，端末に以下のコマンドを入力してtremaを起動した．
```
ruby -r profile ./bin/trema run ./lib/cbench.rb &> result.txt
```

この状態で，他の端末から以下のコマンドを実行して計測を行った．
```
./bin/cbench --port 6653 --switches 1 --loops 10 --ms-per-test 10000 --delay 1000 --throughput
```

これによって得られたprofile情報の一部を以下に示す．
```
 %self      total      self      wait     child     calls  name
  0.48      4.123     0.699     0.000     3.424     5681  *Array#each
  0.16      0.503     0.240     0.000     0.263     2973   BinData::DSLMixin::DSLParser#option?
  0.13      0.355     0.184     0.000     0.171     2281  *BinData::DSLMixin::DSLParser#endian
  0.12      0.707     0.181     0.000     0.527     1073   Gem::Dependency#hash
  0.11      0.290     0.163     0.000     0.127     2461   BinData::SanitizedField#name_as_sym
  0.11      0.163     0.163     0.000     0.000     6356   Symbol#to_sym
  0.10      0.291     0.143     0.000     0.149      857   BinData::Registry#underscore_name
  0.09      0.233     0.135     0.000     0.098     2700   Kernel#initialize_dup
  0.09      1.266     0.135     0.000     1.132        4   Bundler::SpecSet#for
  0.09      0.128     0.128     0.000     0.000     6858   Kernel#nil?
  0.09      2.937     0.126     0.000     2.810      638  *BinData::SanitizedPrototype#initialize
  0.09      0.371     0.125     0.000     0.246      519   Enumerable#sort_by
  0.08      0.124     0.124     0.000     0.000     3413   BinData::DSLMixin::DSLParser#parser_abilities
  0.08      2.032     0.124     0.000     1.908      771  *BinData::SanitizedParameters#sanitize!
```

Array#eachがボトルネックになっていると考えられるため，配列の処理を一考しなくてはならないと考えられる．