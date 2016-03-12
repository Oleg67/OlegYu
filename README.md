# OlegYu
""" Расчет количества повторений последовательности в тексте (ДНК) + определение
максим частого повторения """



def PatternCount(Pattern, Text):
    """Расчет количества повторений последовательности
        -Pattern в тексте -Text(ДНК)"""
    count = 0
    for i in range(len(Text)-len(Pattern)+1):
        if Text[i:i+len(Pattern)] == Pattern:
            count = count+1
    return count

def SymbolArray(Genome, symbol):
     """ возвращает массив поторов элемента генома в прямой и обратной ДНК"""
    array = {}
    n = len(Genome)
    ExtendedGenome = Genome + Genome[0:n//2]
    for i in range(n):
        array[i] = PatternCount(symbol, ExtendedGenome[i:i+(n//2)])
    
    return array

def FrequentWold(Text,k=2,lev=0):
     """определение максим частого повторения длинны k в Text + список наиболее
        частых последовательгостей k длины с частотой более-равно чем (max - lev)"""
     maxicount = 1
     MaXD={}
     MaxDNA = []
     
     for i in range (len(Text)-k+1):
          pattern = Text[i:i+k]
          count = PatternCount(pattern,Text)
          MaXD[pattern] = count
          if count >= maxicount:
               maxicount = count       # max repeat
     for key in MaXD.keys():
         if MaXD[key] >= maxicount-lev :
             MaxDNA.append(key)
                          
     return maxicount,MaxDNA
     
     if __name__=='__main__':
     
     S ='ATCAATGATCAACGTAAGCTTCTAAGCATGATCAAGGTGCTCACACAGTTTATCCACAACCTGAGTGGATGACA\
     TCAAGATAGGTCGTTGTATCTCCTTCCTCTCGTACTCTCATGACCACGGAAAGATGATCAAGAGAGGATGATTTCTTGG\
     CCATATCGCAATGAATACTTGTGACTTGTGCTTCCAATTGACATCTTCAGCGCCATATTGCGCTGGCCAAGGTGACGGA\
     GCGGGATTACGAAAGCATGATCATGGCTGTTGTTCTGTTTATCTTGTTTTGACTGAGACTTGTTAGGATAGACGGTTT\
     TTCATCACTGACTAGCCAAAGCCTTACTCTGCCTGACATCGACCGTAAATTGATAATGAATTTACATGCTTCCGCGAC\
     GATTTACCTCTTGATCATCGATCCGATTGAAGATCTTCAATTGTTAATTCTCTTGCCTCGACTCATAGCCATGATGA\
     GCTCTTGATCATGTTTCCTTAACCCTCTATTTTTTACGGAAGAATGATCAAGCTGCTGCTCTTGATCATCGTTTC'
     # DNA oric
     k=3
     S = 'CGGAGGACTCTAGGTAACGCTTATCAGGTCCATAGGACATTCA'
     count, MaxPattern = FrequentWold(S,k)
     print (MaxPattern,'==>',count)
