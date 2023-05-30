import pandas as pd
df=pd.read_excel('C:\\vagrant-vms\\ht.xlsx')
new_df=df['Additional comments']
pattern = "\[code\]<I>(.*?)</I>\[/code\]"
l=[]
f=[]
for i in new_df:
    match = re.search(pattern,i)
    if match:
        l.append(match.group(1))
for i in l:
    if ", "in i:
        parts=i.split(",")
        for part in parts:
            f.append(part)
    else:
        f.append(i)
freq={}
for item in f:
    if (item in freq):
        freq[item] += 1
    else:
        freq[item] = 1

df =pd.DataFrame (freq.items(), columns=['Group_name', 'Number of occurrences'])
tfile = open('C:\\vagrant-vms\\a.txt', 'w')
tfile.write(df.to_string(index=False))
tfile.close()
