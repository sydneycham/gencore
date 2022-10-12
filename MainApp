import csv
import re
import pandas as pd
from pywebio.input import *
from pywebio.output import *
from pywebio import start_server

def frapp():
    put_markdown('# Professional Info')

	data = input_group("Basic info",[
	    input('Sample Name', name='name', required=True),
	    file_upload('Fragment Peak Table CSV', placeholder='Choose file', accept='.csv', name='fragtable', required=True)
])
print (data['name'])
fragtable = data['fragtable']['content']
FragConcList1 =  []
for line in fragtable.decode().split('\n'):
    x = re.findall('Concentration: ,([0.\a0-9]+)', line)
    if len(x) > 0:
        FragConcList1.append(x[0])

FragConcList1 = [float(x) for x in FragConcList1]
FragSampleList = []
for line in fragtable.decode().split('\n'):
    x = re.findall('_s([0-9]+)', line)
    if len(x) > 0:
        FragSampleList.append(x[0])

FragSampleList
sampleNum = FragSampleList
dict = {'Sample Number': sampleNum}
conc = FragConcList1
dict = {'Concentration': conc}
df = pd.DataFrame(dict)
newcsv = df.to_csv()
newstring = newcsv.encode('utf-8')
with popup('Popup title',):
    put_text("Concentration")
    put_file('name this with .csv', newstring)
    put_text('me done')

put_text('me done')
