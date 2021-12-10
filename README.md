# Metric-Dimension

import numpy as np
import itertools as it

f = open("wil5.txt", "w") 
print("Dimensi metrik graf G")
f.write("Dimensi metrik graf G")
n=int(input("Input order graf G ="))
f.write("\n Order graf G = {}".format(n))

incident=[]
nn=(n,n)
jarak=np.zeros(nn)
ver=[]
adj=np.zeros(nn)
jdiincident=0
nilaibasis=0
listbasis=[]

# mendefinisikan keterhubungan titik-titik pada graf G
for i in range (n):
    print("derajat titik ",i)
    der=int(input("="))
    print("Titik yang terhubung dengan titik ",i)
    for j in range(der):
        konek=int(input("= "))
        adj[i][konek]=adj[konek][i]=1

# menyusun matriks adj
for k in range(n):
    ver.append(k)
    
# menampilkan matriks adjacency
print("Vertex dari Graf adalah ",ver)
f.write("\n Vertex dari Graf adalah {}".format(ver))
print("Matrik Adjacency")    
for i in range (n):
    print(adj[i])         

incident=[]
# menentukan jarak antar titik
jarak=np.zeros(nn)
for i in range (n):
    for j in range (i):
        print ("\nJarak vertex ",i," dan ",j )
        for p in range (n):
            if (adj[i][p]==1):
                print(i," terhubung langsung dengan titik",p)
                incident.append(p)
       
        step=1
        pincident=len(incident)
        nilai=1
        while(nilai==1):
            pincident=len(incident)
            if (j in incident):
                # menentukan jarak titik i dan j
                jarak[i][j]=jarak[j][i]=step
                print("Jaraknya adalah ",step)
                nilai=0
            else:
                for titik in range(pincident):
                    for vertex in range(n):
                        if(adj[incident[titik]][vertex]==1):
                            incident.append(vertex)
            step+=1
        incident=[]

# menampilkan tabel jarak antar titik
print("\nTabel Jarak =")
for i in range (n):
    print(jarak[i])
   
print("\n Mendefinisikan Himpunan Pembeda")
#untuk kardinalitas 1 sampai n-1
for kar in range(1,n):
    comb=it.combinations(ver,kar)
    print("\nUntuk Kardinalitas ",kar)
    sizerep=(n,kar)
    repre=np.zeros(sizerep)
    # mencari koordinat tiap kombinasi
    for i in list(comb):
        for tiap in range (kar):
            for j in range (n):
                repre[j][tiap]=jarak[i[tiap]][j]
                
        print("\nRepresentasi titik dengan kombinasi ",i)
        
        nilaibasis=0
        for k in range (n):
            print("titik ",k," = ",repre[k])
        # mengecek apakah ada koordinat yang sama antar titik
        for titik in range (n):
            for sama in range (titik):
                if(np.array_equal(repre[titik],repre[sama])):
                    print("koordinat yang sama yaitu ",titik," dan ",sama)
                    nilaibasis=1
        
        # mendefinisikan kombinasi himpunan pembeda            
        if(nilaibasis==0):
            listbasis.append(i)
            
    if(len(listbasis)!=0):
        break
    
print("dim(G) = ",kar)
f.write("\n dim(G) = {}".format(kar))
print("Kombinasi himpunan pembeda yang mungkin")
f.write("\n Kombinasi himpunan pembeda yang mungkin")
for m in range (len(listbasis)):
    print(listbasis[m])
    f.write("\n {}".format(listbasis[m]))
    
f.close()
