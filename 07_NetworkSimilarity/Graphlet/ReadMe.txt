Steps

Network comparison was done with a program from: http://www0.cs.ucl.ac.uk/staff/natasa/GCD/index.html

In order to compare networks, I did the following steps and adjustments: 

1. Transform networks into Leda (.gw) format: no problem with the igraph function, e.g. in R

2. Compute the graphlet degree vector signatures of each network using the provided script: "python count.py my_network.gw"
-> I am working with a MAC and a newer python version. I adjusted two lines:
-> in line 86 I added parenthesis for print
-> execution error for OCRA (line 98 and 99)
-> I downloaded the orca program from: https://github.com/thocevar/orca, and adjusted the python script in line 98 from:
"cmd = './orca 5 ' + outputFileName + ' ' + tempNdump2File"
to
"cmd = './../orca-master/orca.exe node 5 ' + outputFileName + ' ' + tempNdump2File"

3. Compute GCD-11, (all networks and their signature files must be in the same folder):  "python network_folder gcd11 n", where n=#threads
-> the webpage missed the name of pj script, it should be: "python networkComparison.py network_folder gcd11 n"
-> line 460, 464, and 482 produce an error since the condition is stated as "if signs1[i] <> 0:" and if signs2[i] <> 0:" and "if line.strip() <> '':" and "<>" has been removed in newer version, it works with "!="
-> in about >30 cases I added parenthesis for print
-> in >20 cases: "Queue" now lower case letter: "queue"
-> I had to adjust line 256-258 because of changes to dictionary. The following should do what was intended:
```
	# Write the distances among networks
	for i in list(networkNames):
		toWrite = i + '\t'
		for val in matrix[list(networkNames).index(i)]:
			toWrite += str(val) + '\t'
		fWrite.write(toWrite.rstrip() + '\n')
```