#Jader Duarte questão 1
# Não funciona direito mas conceitualmente é quase lá 
class TreeNode:
    def __init__(self, val=0):
        self.val = val
        self.left = None
        self.right = None

# no git tinha:
def insert_node(root, value):
        current_node = root
        while current_node:
            if value < current_node.val:
                if current_node.left is None:
                    current_node.left = TreeNode(value)
                    break
                current_node = current_node.left
            elif value > current_node.val:
                if current_node.right is None:
                    current_node.right = TreeNode(value)
                    break
                current_node = current_node.right
            else:
                # Duplicate value found, return None to indicate an error
                print(f"Duplicate value {value} found. BST cannot have duplicate values.")
                return None
        return root

def is_balanced(root):
    max= 0
    min= 0
    min_is_base= True
    proximo=[]
    contar=0
    atual=[root]
    ja_foi=True #pra entrar no loop
    while ja_foi or atual!=[]: # no final do loop os galhos seguintes serão atual. portanto quando terminar de percorrer atual = []
        ja_foi=False 
        n_contei_nova_camada=True
        for i in atual:
            proximo=[]
            if i.left:
                proximo.append(i.left)
                if n_contei_nova_camada:
                    contar+=1
                    n_contei_nova_camada=False
            elif min_is_base:
                min=1+ contar
                min_is_base= False
            if i.right:
                proximo.append(i.right)
                if n_contei_nova_camada:
                    contar+=1
                    n_contei_nova_camada=False
            elif min_is_base:
                min= contar+1
                min_is_base= False
        atual= proximo
    max= int(contar)
    if max-min>1:
        return False
    else:
        return True
    
# Criando a árvore e testando
root = TreeNode(10)
insert_node(root, 5)
insert_node(root, 15)
insert_node(root, 3)
insert_node(root, 7)
insert_node(root, 12)
insert_node(root, 18)

# Testando se a árvore está balanceada
print(is_balanced(root))  # Deve retornar True

# Inserindo mais nós para desequilibrar a árvore
insert_node(root, 2)
insert_node(root, 1)  
# Adicionando um nós que desequilibra a árvore

# Testando novamente
print(is_balanced(root))  # Deve retornar False

# Questão 2
import random as rd
class Pilha:
    def __init__(self,l):
        self.coord = l
    
    def pop(self):
        n=rd.randint(0,len(self.coord)-1)
        x= self.coord[n]
        self.coord[n]=self.coord[0]
        self.coord.pop(0) # Assumindo que nesta pilha, cujo nome aparentemente é uma pegadinha, a ordem não importa.
        return x
    def push(self,A):
        self.coord.append(A)
