# test.io
testing
# csv2xml.py
# FB - 201010107
# First row of the csv file must be header!
 
# example CSV file: myData.csv
# id,code name,value
# 36,abc,7.6
# 40,def,3.6
# 9,ghi,6.3
# 76,def,99
 
import csv
 
csvFile = 'myData.csv'
xmlFile = 'myData.xml'
 
csvData = csv.reader(open(csvFile))
xmlData = open(xmlFile, 'w')
xmlData.write('<?xml version="1.0"?>' + "\n")
# there must be only one top-level tag
xmlData.write('<csv_data>' + "\n")
 
rowNum = 0
for row in csvData:
    if rowNum == 0:
        tags = row
        # replace spaces w/ underscores in tag names
        for i in range(len(tags)):
            tags[i] = tags[i].replace(' ', '_')
    else: 
        xmlData.write('<row>' + "\n")
        for i in range(len(tags)):
            xmlData.write('    ' + '<' + tags[i] + '>' \
                          + row[i] + '</' + tags[i] + '>' + "\n")
        xmlData.write('</row>' + "\n")
            
    rowNum +=1
 
xmlData.write('</csv_data>' + "\n")
xmlData.close()


### 2
import csv 
reader = csv.reader(open("test.csv")) 
writer = open("contacts.xml","w") 
for name, phone, adress in reader: 
     writer.write("<item>\n" + 
                 "\t<name>"+name+"</name>\n" + 
                 "\t<phone>"+phone+"</phone>\n" + 
                 "\t<adress>"+adress+"</adress>\n" + 
                 "</item>\n") 
 writer.close() 
 
 
 
 ###3
 import csv, os
from xml.dom.minidom import Document

#prfixFile = "creature_data"

def createXMLFile(filePrefix):
    csvFile = open(filePrefix+'.csv');
    headLine = csvFile.readline()
    #print headLine
    typeList = headLine.split(',')

    doc = Document()
    dataRoot = doc.createElement(filePrefix+'List')
    dataRoot.setAttribute('xmlns:xsi', "http://www.w3.org/2001/XMLSchema-instance")
    dataRoot.setAttribute('xsi:schemaLocation', filePrefix+'.xsd')
    doc.appendChild(dataRoot)

    csvReader = csv.reader(csvFile)
    for line in csvReader:
        #print line
        dataElt = doc.createElement(filePrefix)
        for i in range(len(typeList)):
            dataElt.setAttribute(typeList[i], line[i])
        dataRoot.appendChild(dataElt)

    xmlFile = open(filePrefix+'.xml','w')
    xmlFile.write(doc.toprettyxml(indent = '\t'))
    xmlFile.close()

def main():
    for root, dirs, files in os.walk(os.getcwd()):
        for fname in files:
            index = fname.find('.csv')
            if index > 0:
                #print index, fname[:index]
                createXMLFile(fname[:index])
                print "Transform " + fname + " OK!"

if __name__ == '__main__':
    main()
    input("Game Over!")
    
    
    
    
    ####3
    #!/usr/bin/python

#CSVtoXML.py

#encoding:utf-8
import csv, os
from xml.dom.minidom import Document

#prfixFile = "creature_data"

def createXMLFile(filePrefix):
    csvFile = open(filePrefix+'.csv');
    headLine = csvFile.readline()
    #print headLine
    typeList = headLine.split(',')

    doc = Document()
    dataRoot = doc.createElement(filePrefix+'List')
    dataRoot.setAttribute('xmlns:xsi', "http://www.w3.org/2001/XMLSchema-instance")
    dataRoot.setAttribute('xsi:schemaLocation', filePrefix+'.xsd')
    doc.appendChild(dataRoot)

    csvReader = csv.reader(csvFile)
    for line in csvReader:
        #print line
        dataElt = doc.createElement(filePrefix)
        for i in range(len(typeList)):
            dataElt.setAttribute(typeList[i], line[i])
        dataRoot.appendChild(dataElt)

    xmlFile = open(filePrefix+'.xml','w')
    xmlFile.write(doc.toprettyxml(indent = '\t'))
    xmlFile.close()

def main():
    for root, dirs, files in os.walk(os.getcwd()):
        for fname in files:
            index = fname.find('.csv')
            if index > 0:
                #print index, fname[:index]
                createXMLFile(fname[:index])
                print "Transform " + fname + " OK!"

if __name__ == '__main__':
    main()
    input("Game Over!")
    
    
    
    ####4
    #!/usr/bin/python
#XMLtoCSV.py
#encoding:utf-8
import csv, os
from xml.dom.minidom import parse

def createCSVFile(filePrefix):
    csvFile = open(filePrefix+'.csv', 'wb')  #注意是二进制写入，否则会有多余空格
    csvWriter = csv.writer(csvFile)
    bWriteHead = False
    xmlFile = open(filePrefix+'.xml')
    domTree = parse(xmlFile)
    #print domTree
    root = domTree.documentElement
    #print dir(collection)
    for node in root.childNodes:
        if node.nodeType == node.ELEMENT_NODE:
            #print node.nodeName
            element = {}
            for key in node.attributes.keys():
                value = node.attributes.get(key).value
                element[key] = value
            if len(element) > 0:
                if bWriteHead == False:
                    csvWriter.writerow(tuple(element.keys()))
                    bWriteHead = True
                csvWriter.writerow(tuple(element.values()))
            else:
                print node.attributes
            
    csvFile.close()
    xmlFile.close()
    

def main():
    for root, dirs, files in os.walk(os.getcwd()):
        print root, dirs, files
        for fname in files:
            index = fname.find('.xml')
            if index > 0:
                #print index, fname[:index]
                createCSVFile(fname[:index])
                print "Transform " + fname + " OK!"

if __name__ == '__main__':
    main()
    input("Game Over!")
    
    
    
    
    
    #####6
    #!/usr/bin/python
 
#CSVtoXML.py
 
#encoding:utf-8
import csv, os
from xml.dom.minidom import Document
 
#prfixFile = "creature_data"
 
def createXMLFile(filePrefix):
    csvFile = open(filePrefix+'.csv');
    headLine = csvFile.readline()
    #print headLine
    typeList = headLine.split(',')
 
    doc = Document()
    dataRoot = doc.createElement(filePrefix+'List')
    dataRoot.setAttribute('xmlns:xsi', "http://www.w3.org/2001/XMLSchema-instance")
    dataRoot.setAttribute('xsi:schemaLocation', filePrefix+'.xsd')
    doc.appendChild(dataRoot)
 
    csvReader = csv.reader(csvFile)
    for line in csvReader:
        #print line
        dataElt = doc.createElement(filePrefix)
        for i in range(len(typeList)):
            dataElt.setAttribute(typeList[i], line[i])
        dataRoot.appendChild(dataElt)
 
    xmlFile = open(filePrefix+'.xml','w')
    xmlFile.write(doc.toprettyxml(indent = '\t'))
    xmlFile.close()
 
def main():
    for root, dirs, files in os.walk(os.getcwd()):
        for fname in files:
            index = fname.find('.csv')
            if index > 0:
                #print index, fname[:index]
                createXMLFile(fname[:index])
                print "Transform " + fname + " OK!"
 
if __name__ == '__main__':
    main()
    input("Game Over!")



###7
import csv 
reader = csv.reader(open("test.csv")) 
writer = open("contacts.xml","w") 
for name, phone, adress in reader: 
writer.write("<item>\n" + 
"\t<name>"+name+"</name>\n" + 
"\t<phone>"+phone+"</phone>\n" + 
"\t<adress>"+adress+"</adress>\n" + 
"</item>\n") 
writer.close() 


    
    
