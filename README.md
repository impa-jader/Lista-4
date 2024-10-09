#Jader Duarte 
# Questão 1 #

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
        contar+=1 
        proximo=[]
        for i in atual:
            if i.left:
                proximo.append(i.left)
            elif min_is_base:
                min=contar
                min_is_base= False
            if i.right:
                proximo.append(i.right)
            elif min_is_base:
                min= contar
                min_is_base= False
        print([i.val for i in atual]) #teste 
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

## Questão 2 ##
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

#### Questão 4 ####
# Não estou familharizado com os tipos de distribuição desta questão. Portanto não sei dizer se está funcionando corretamente
import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import uniform, norm, t
from scipy.spatial import ConvexHull

def Sort_points():
    N= int(input("Quantos pontos \n"))
    pick = input("""Escolha a distribuição: 
              (1) Uniforme
              (2) Normal
              (3) Student t  \n""")
    if pick== "1": # Uniforme
        x = uniform.rvs(loc=-1, scale=2, size=N)  # Gera valores entre -1 e 1
        y = uniform.rvs(loc=-1, scale=2, size=N)
    if pick== "2": # Normal
        x = norm.rvs(loc=0, scale=0.5, size=N)  # Média 0, desvio padrão 0.5
        y = norm.rvs(loc=0, scale=0.5, size=N)
    if pick== "3": # Student t
        x = t.rvs(df=1, loc=0, scale=0.5, size=N)  # Média 0, desvio padrão 0.5
        y = t.rvs(df=1, loc=0, scale=0.5, size=N)
        

    return x,y

coords=Sort_points()
plt.scatter(coords[0],coords[1])
plt.title('Pontos Sorteados')
plt.xlabel('Eixo x')
plt.ylabel('Eixo y')
plt.show()

##### Questão 5 #####

def desfeixo_convexo(pontos):
  hull = ConvexHull(pontos)
  return pontos[hull.vertices]
