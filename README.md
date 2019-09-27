# L1_embeded_Language

The goal is to do a complete analysis include check_isMyLanguage, infer_type_check, and infer_memory on the programme written in my sub_language

By overridding the Visit node function in python and recursively call the function on the node and child node,we can easily check if it is under the rule of my sub language.\n
By using the evm={} to store the necessary information for variables we create, so that we can get the information later when the variable is used afterwards.


there are three parts:
1.check_isMyLanguage: check if every part eg. ops is in the set of My language token,
                      check the attribute to check if the only function call is pd.DataFrame and pd.concat
                 
2.type_infer_check: checking every detail to ensure that + - can only be operated in List, Tuple or DataFrame
                    boolop  can only be operated on bool
                    the concat function can only be List of DataFrame
                    the DataFrame can only be Tuple or List or DataFrame
                    recursively, we can check all.
  approach: maintain the evm={'id':type} to store all the variable type we create eg. x, so we can infer the type of eg. x+1 afterwards.
  the result is a list of type infer for every statement in the programme.
                  
3.infer_memory: in the recursively way, we can check all the expression and variable memory cost, then add up.
  approach: for the variables created: maintain the evm={'id':number of bytes} to store all the variable bytes we create eg. x, so we                can infer the memory of eg.x+1 easily
    



BNF:

program ::= statement
           |statement program 
statement =Return(expr)
     | Assign(expr* targets, expr value)
     | Expr(expr value)
        
expr = BinOp(expr left, operator op, expr right)
         |BoolOp(boolop op, expr* values)
         | Call(expr Func, expr* args, keyword* keywords)
         | Positive_Int(object n)
         |Str(string s)
         | Attribute(expr value, identifier Attr)
         | Name(identifier id)
         | List(expr* elts)
         | Tuple(expr* elts)
         
operator ::= Add | Sub 
boolop::= And|Or
Attr ::= concat|DataFrame  
arguments = (arg* args)
arg = (identifier arg, expr? annotation)

