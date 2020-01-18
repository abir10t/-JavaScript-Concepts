# -JavaScript-Concepts

## 3.11 scope chain
function saymyname(){
    var a='a';
    return function findname(){

        var b='b';
          console.log(b);
        return function printname(){
            var c='c';
            return 'life';


        }
    }

}
saymyname()()();
result -> b and life;
find name function is written in saymyname function.here find name function lexical environment is printname function.print name function lexical environment is findname function .so here's the scope work.but we can't find a result of c variable if we (console.log(c)) at 9 number line. 





