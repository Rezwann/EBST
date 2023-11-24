class STNode:
    def __init__(self,d,l,m,r):
        self.data = d
        self.left = l
        self.right = r
        self.fwd = m
        self.mult = 0
          
    # prints the node and all its children in a string
    def __str__(self):
        st = "("+str(self.data)+", "+str(self.mult)+") -> ["
        if self.left != None:
            st += str(self.left)
        else: st += "None"
        if self.fwd != None:
            st += ", "+str(self.fwd)
        else: st += ", None"
        if self.right != None:
            st += ", "+str(self.right)
        else: st += ", None"
        return st + "]"
    
class StringTree:
    def __init__(self):
        self.root = None
        self.size = 0
        
    def __str__(self):
        return str(self.root)


    def add(self,st):
        if st == "":
            return None
        if self.root == None:
            self.root = STNode(st[0],None,None,None)
        ptr = self.root
        for i in range(len(st)):
            d = st[i]
            while True:
                if d == ptr.data:
                    break
                elif d < ptr.data:
                    if ptr.left == None:
                        ptr.left = STNode(d,None,None,None)
                    ptr = ptr.left
                else:
                    if ptr.right == None:
                        ptr.right = STNode(d,None,None,None)
                    ptr = ptr.right
            if i < len(st)-1 and ptr.fwd == None:
                ptr.fwd = STNode(st[i+1],None,None,None)
            if i < len(st)-1:
                ptr = ptr.fwd
        ptr.mult += 1
        self.size += 1        
    def addAll(self,A):
        for x in A: self.add(x)
        
    def printAll(self):
        def printFrom(ptr,s):
            if ptr == None: return
            s0 = s + ptr.data
            for i in range(ptr.mult,0,-1): print(s0)
            if ptr.left != None: printFrom(ptr.left,s)
            if ptr.fwd != None: printFrom(ptr.fwd,s+ptr.data)
            if ptr.right != None: printFrom(ptr.right,s)
        printFrom(self.root,"") 
        
    def CheckTreeIsEmpty(self, st):
        inv = []
        occurrences = 0
        def emptyFrom(ptr, s, inv):
            if ptr is None: return
            s0 = s + ptr.data
            for i in range(ptr.mult, 0, -1):
                inv[len(inv):] = [s0]
            if ptr.left != None: emptyFrom(ptr.left, s, inv)
            if ptr.fwd != None: emptyFrom(ptr.fwd, s + ptr.data, inv)
            if ptr.right != None: emptyFrom(ptr.right, s, inv)
        emptyFrom(self.root, "", inv)
        if not inv: 
            return True            
        else:
            return False
        






    def count(self, st): # count
        inv = []
        occurrences = 0
        def countFrom(ptr, s, inv):
            if ptr is None: return
            s0 = s + ptr.data
            for i in range(ptr.mult, 0, -1):
                inv[len(inv):] = [s0]
            if ptr.left != None: countFrom(ptr.left, s, inv)
            if ptr.fwd != None: countFrom(ptr.fwd, s + ptr.data, inv)
            if ptr.right != None: countFrom(ptr.right, s, inv)
        countFrom(self.root, "", inv)
        for i in inv:
            if i == st:
                occurrences+=1
        return occurrences    
    
    def remove(self, st): # remove
        def deleteNode(self, ptr, val):
            if ptr == None:
                return ptr
            if ptr.right is None:
                return ptr.left
            if ptr.left is None:
                return ptr.right
            elif val > ptr.data:
                ptr.right = self.deleteNode(ptr.right, val)
            elif val < ptr.data:
                ptr.left = self.deleteNode(ptr.left, val)
            else:
                if ptr.left == ptr.right == None:
                    ptr = None
                elif ptr.left == None:
                    ptr = ptr.right
                elif ptr.right == None:
                    ptr = ptr.left
                else:
                    current = ptr.right
                    while(current.left!=None):
                        current = current.left
                    ptr.mult = current.mult
                    ptr.data = current.data
                    ptr.right = self.deleteNode(ptr.right, current.data)
            return ptr


        def delete(ptr, st):
            if ptr == None:
                return ptr
            if st == None:
                return ptr
            if st == ptr.data and (ptr.mult != 0): # case of one char argument
                ptr.mult -= 1
                self.size -= 1
            elif st[0] < ptr.data:
                ptr.left = delete(ptr.left, st)
            elif st[0] > ptr.data:
                ptr.right = delete(ptr.right, st)
            else:
                ptr.fwd = delete(ptr.fwd, st[1:]) # all except first char
            if ptr.mult != None: # checking if it is okay to delete
                return ptr
            if ptr.fwd != None:
                return ptr
            else:
                deleteNode(ptr)
        self.root = delete(self.root, st)
        
    def max(self): # max
        inv = []
        occurences = 0
        def maxFrom(ptr, s, inv):
            if ptr is None: return
            s0 = s + ptr.data
            for i in range(ptr.mult, 0, -1):
                inv[len(inv):] = [s0]
            if ptr.left != None: maxFrom(ptr.left, s, inv)
            if ptr.fwd != None: maxFrom(ptr.fwd, s + ptr.data, inv)
            if ptr.right != None: maxFrom(ptr.right, s, inv)
        maxFrom(self.root, "", inv)
        for i in range(len(inv)):                                 
            for j in range(len(inv) - 1):                         
                if inv[j] > inv[j + 1]:
                    inv[j] = inv[j + 1]     
                    inv[j + 1] = inv[j]     
        if not inv:
            return None
        else:
            return inv[-1]
