import numpy as np
import csv
import itertools

## SET VARIABLES
#n is number of random variables 
n=5
fieldsize=n
##for i in range(1,n+1):
##    for j in range(i+1,n+1):
##        print str(i)+str(j)

def cycshift(strelement,fieldsize):
    l=str()
    element=list(strelement)
    for i in range(len(element)):
        if int(element[i])==fieldsize:
            element[i]=1
        else:
            element[i]=int(element[i])+1
        element.sort()
    for i in element:
        l+=str(i)
    return l


## The next function, strcheck(s,liststr) is to check if the elements of s is in
##  the list of liststr; if so it will put 1 in that element of the list other wise 0

def strcheck(s,liststr):
    lists=list(s)
    output=[]
    for i in range(len(liststr)):
        temp=1  #preset that elements of 's' are not in the list element i
 
        for j in range(len(s)):
            if lists[j] in liststr[i]:
                temp*=1
            else:
                temp*=0
        output.append(temp)
    return output
                


print strcheck('er',['qer','ety','eq','re'])   



def union(a, b):
    """ return the union of two lists """
    lsa=list(a)
    lsb=list(b)
    ls=list(set(lsa) | set(lsb))
    intls=[int(l) for l in ls]
    intls.sort()
    g=str()
    for l in intls:
        g+=str(l)
    return g


#the output shows that if string element is in the lists of the listlist(which is a list of list)
'''findmx('1',[['31'],['1','13']])
 returns [1, 1]'''
def findmx(element,listlist):
    outls=[]
    for i in range(len(listlist)):
        if sum(strcheck(element,listlist[i]))>=1:
            outls.append(1)
        else:
            outls.append(0)
    return outls
        

def findx(element,listlist):
    outls=[]
    for i in range(len(listlist)):
        if sum(strcheck(element,listlist[i]))==1:
            out= i
            break;
        else:
            out=-1
    return out
        
##        
##        else:
##            return -1
##     

    ## Code to print combinations-------------------------------
#print cycshift('125',5)
l=str()
initlist=[]
for i in range(1,n+1):
    initlist.append(str(i))
    #l+=str(i)
    print l
Hlist=[]



wind=1
temp=[]
Comblist=[[],initlist]

for e in range(1,wind+1):
    l+=str(e)  # first make the first element of the combination as a string

itr=1

while True:
        temp=[]
        for i in Comblist[itr]:
          #print i
          for j in range(int(list(i).pop())+1,n+1):

            temp.append(i+str(j))

        if temp==[]:
            break;

            

        Comblist.append(temp)
        #print Comblist
        itr+=1
print Comblist
##----------------------------------------------------------
# next is to alternate in elements to get all combinations

##    itr=len(Comblist)-1  # this is a pointer to the last combinations list with wind-1 elements    
##    for i in Comblist[itr]:
##        for j in range(1,n+1):
##            
##            temp.append(i+str(j))
##
##            
##        
##    Comblist.append(temp)
##    itr+=1
##
##    wind+=1
##
####for i in range(1,n+1):
####    templist=list(itertools.combinations(l,i))
####    print templist
####    
##-----Improving the combination to Print Orbits------
HOrbits=[[],[[],initlist]]
ct=0
for i in range(2,len(Comblist)):
    Comblist_i=Comblist[i][:]
    Comblist_i.reverse()
    HOrbits.append([[]])
    
    while Comblist_i!=[]:
        temp=[]
        newelement=Comblist_i.pop()
        
    
        temp.append(newelement)
        #newelement=cycshift(newelement,n)
        flg=True
        while True:
            
            shifel=cycshift(newelement,n)
            if ( shifel in Comblist_i):
                newelement=shifel 
                temp.append(shifel)
                Comblist_i.remove(shifel)
            else:
                break;
        HOrbits[i].append(temp)

print HOrbits

print findmx('12',HOrbits[3])

### ____________ Print Inequalities--------------
l=0
orbitleaders=[]
for i in HOrbits:
    if i!=[]:
        orbitleaders.append([item[0] for item in i if item!=[]])   ##'Here I just get one element from each orbit as
                                    #Orbit leaser or coset.
                                    # Remember that i[0]=[]
        l+=len(i)-1
    

print orbitleaders
temp_ineq=[0]*l

newinequality=temp_ineq[:]
inequlaities=[]
                ##_____H(X_i|X_{rest})>=0---------
newinequality[len(temp_ineq)-1]=1
newinequality[len(temp_ineq)-2]=-1

inequlaities.append(newinequality)
print inequlaities
newinequality=temp_ineq[:]

                ##---I(X_i,X_j)=>0-------------
for i in range(1,len(HOrbits[2])):
    newinequality[0]=1
    newinequality[i]=-1
    inequlaities.append(newinequality)
    newinequality=temp_ineq[:]
print inequlaities

                ##---I(X_i,X_j|X_k,...)

p=orbitleaders[:]
Comblist.remove([])
HOrbits.remove([])
ind=0
for i in range(len(p)-2):
    '''here we choose each element of orbitleaders'''
    ind+=len(p[i])
    for j in range(len(p[i])):
        UP=[]
        for k in range(len(strcheck(p[i][j],Comblist[i+1]))):
            if strcheck(p[i][j],Comblist[i+1])[k]!=0:
##        for k in range(len(Comblist[i+1])):
##            if sum(strcheck(p[i][j],Comblist[i+1][k]))>=1:
                UP.append(Comblist[i+1][k])
            #UP contains elements with one more letter
            for item1 in UP:
                for item2 in UP:
                    
                    if (item1!=item2):
                        newinequality=temp_ineq[:]
                        newinequality[ind+findx(item1,HOrbits[i+1])-1]+=1
                        newinequality[ind+findx(item2,HOrbits[i+1])-1]+=1
                        newinequality[ind+len(p[i+1])+findx(union(item1,item2),HOrbits[i+2])-1]=-1
                        newinequality[ind-len(p[i])+j]=-1
                       
                        #newinequality[i-1+len(p[i])+findx(item1,HOrbits[i+1])]+=1
                        #newinequality[i-1+len(p[i])+findx(item2,HOrbits[i+1])]+=1
                        #newinequality[i+len(p[i+1])+findx(union(item1,item2),HOrbits[i+2])]=-1
                        #newinequality[i+j]=-1
                        if newinequality not in inequlaities:
                        
                            inequlaities.append(newinequality)
                                      
print inequlaities                   
        
               
        

        

