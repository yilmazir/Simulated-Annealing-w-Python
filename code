import multiprocessing
import numpy as np
import math
import time

class SimulatedAnnealing:
    def __init__(self, x, M, T, n, L, E):
        self.initialX = x
        self.M = M
        self.T = T
        self.n = n
        self.L = L
        self.E = E

    def calculateLengthOfTour(self, tour):
        sumDistance = 0
        for ind in range(len(tour)):
            v_1 = tour[ind]

            if (ind == (len(tour) - 1)):
                v_2 = tour[0]
            else:
                v_2 = tour[ind + 1]

            sumDistance += self.M[v_1][v_2]

        return sumDistance


    def generateNewTour(self, x):
        rangeForRandomNumbers = np.arange(len(x))
        uniqueRandomIndexs = np.random.choice(rangeForRandomNumbers, 2, replace=False)
        n1 = uniqueRandomIndexs[0]
        n2 = uniqueRandomIndexs[1]

        y = np.copy(x)
        temp = y[n1]
        y[n1] = y[n2]
        y[n2] = temp

        return y

    def run(self):
        x = self.initialX
        fx = self.calculateLengthOfTour(x)
        T = self.T
        E = self.E
        while T > E:
            for i in range(L):
                y = self.generateNewTour(x)
                fy = self.calculateLengthOfTour(y)

                if (fy < fx):
                    x = y
                    fx = fy
                else:
                    randomNum = np.random.rand()
                    if (randomNum < math.exp(-(fy - fx) / T)):
                        x = y
                        fx = fy

            T = 0.95 * T 


        return x, fx

a = np.loadtxt('29_cities.txt')
b = np.loadtxt('42_cities.txt')
c = np.loadtxt('76_cities.txt')

txts = [a, b, c]

for txt in txts:
  start_time = time.time()
  A = len(txt)

  list = []
  lista = []

  selected_A = A*[0]
  no_edge = 0
  selected_A[0] = True

  sum = 0

  while (no_edge < A - 1):
      minimum = np.inf
      x = 0
      y = 0
      for i in range(A):
          if selected_A[i]:
              for j in range(A):
                  if ((not selected_A[j]) and txt[i][j]):
                      if minimum > txt[i][j] and not list.__contains__(i):
                          minimum = txt[i][j]
                          x = i
                          y = j
              list.append(i)
      selected_A[y] = True
      no_edge += 1

      s = int(txt[x][y])

      sum = sum + s

      if lista.__len__() == 0:
          lista.append(x)
          lista.append(y)
      else:
          lista.append(y)
  if lista.__len__() == A:
      lista.append(int(txt[0][0]))
  sum = sum + int(txt[0][y])

  print("Initial Solution:")

  print(lista)
  print("  Total Distance:", sum)
  lista.pop() 
  T = 3
  n = lista.__len__()
  L = int(A) 
  E = 10 ** -2


  x = np.array(lista) 
  M = txt 
  M = M.reshape(n, n) 
  SA = SimulatedAnnealing(x, M, T, n, L, E) 

  print( )
  print("According to Simulated Annealing:")

  bestx, bestfx = SA.run() 
  list_x = bestx.tolist() 
  list_x.append(list_x[0])
  print("Best tour: ", list_x, "Best fx: ", bestfx)
  print()

  print("Time: %s seconds" % (time.time() - start_time))
  print()
  print("=====================================\n")

def relaxation():
    a = np.loadtxt('29_cities.txt')
    b = np.loadtxt('42_cities.txt')
    c = np.loadtxt('76_cities.txt')

    txts = [a, b, c]
    names = ["29 Cities", "42 Cities", "76 Cities"]
    name_index = 0

    for txt in txts:
        print("=====================================")
        print(names[name_index])
        name_index += 1
        
        min_edges = []
        lb = 0

        skipped_edges = []

        for i in range(len(txt)):
            local_min = np.inf
            min_x = 0
            min_y = 0

            for j in range(len(txt)):

                if i == j:
                    continue

                elif j > i:
                    if txt[i][j] < local_min:
                        local_min = txt[i][j]
                        min_x = i
                        min_y = j
                        min_edges.append((i, j))
                        skipped_edges.append((j, i))

                else:
                    if txt[i][j] < local_min and (i, j) not in skipped_edges:
                        local_min = txt[i][j]
                        min_x = i
                        min_y = j
                        min_edges.append((i, j))

            lb += local_min

        print("Lower Bound: ", lb)
        print("=====================================")
print("\n==============================================\n")
print("RELAXATION RESULTS SHOWN IN BELOW: ")
relaxation()
