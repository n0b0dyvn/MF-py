#!/usr/bin/env python2
import subprocess
import urllib2
import shlex
import sys

"""
###Case many link mediafire
class lstLink:								
	def __init__(self):
		self.lst = lstsysargv
		self.lst.pop(0)
		self.filters()
	### Remove all other link and correct link
	def filters(self):
		tmp = []
		for i in self.lst:
			if 'mediafire' in i:
				tmp+=[i]
		for i in xrange(0,len(tmp)):
			if 'http://' != tmp[i][:len('http://')]:
				tmp[i]= 'http://' + tmp[i]
		self.lst = tmp
	def display(self):
		print self.lst
"""
### case 1 link Download
class linkDownload:									
	def __init__(self,link):
		self.link = link
		self.urlLast = ''
		self.fileName = ''
		self.linkDownload = ''
		self.getlinkDownload()
	def getlinkDownload(self):
		try:
			source = urllib2.urlopen(self.link).read()
		except:
			print "Your Link is Wrong Code 1"
			sys.exit(0)
		self.fileName = source[source.index('<title>')+len('<title>'):source.index('</title>')]
		self.urlLast = self.link[self.link.index('?')+1:]

		lDi = source.index('kNO = "')+len('kNO = "')
		self.linkDownload = source[lDi:]
		lDi = self.linkDownload.index('";')
		self.linkDownload = self.linkDownload[:lDi]
		self.link=self.linkDownload
	
	def downloadFile(self):
		command = 'wget ' + self.link
		args = shlex.split(command)
		proID = subprocess.Popen(args)
		proID.wait()
	def display(self):
		print self.urlLast,self.fileName

###Case Folder
#http://www.mediafire.com/api/folder/get_info.php?r=vdxs&folder_key=wj34bzbhdirob&;response_format=json&version=1
class folderMF:
	def __init__(self,link):
		self.link = link[link.index('?')+1:]
		self.lstFile = self.getLst()
	def getLst(self):
		try:
			source = str(urllib2.urlopen('http://www.mediafire.com/api/folder/get_info.php?r=vdxs&folder_key=%s&;response_format=json&version=1' %self.link).read())
		except:
			print "Your Link is Wrong. Code 2"
			sys.exit(0)
		lst =[]
		while '<quickkey>' in source :
			index = source.index('<quickkey>')+len('<quickkey>')
			source = source[index:]
			lst += ['http://www.mediafire.com/?'+source[:15]]
		return lst
	def display(self):
		print self.lstFile

if __name__ == '__main__':
	### No argument give , so we exit program
	if len(sys.argv)!=2:
		print "Useage: %s <linkMediafire>" % sys.argv[0]
		print "or"
		print "Useage: python2 %s <linkMediafire>" % sys.argv[0]
		sys.exit(0)
	link = sys.argv[1]
	urlLast = link[link.index('?')+1:]
	if 'http://' != link[:len('http://')]:
		link= 'http://' + link
	try:
		source = str(urllib2.urlopen('http://www.mediafire.com/api/folder/get_info.php?r=vdxs&folder_key=%s&;response_format=json&version=1' % urlLast).read())
		for i in folderMF(link).lstFile:
			print
			downLoad = linkDownload(i)
			print "\t\t\t********DOWNLOADING FILE %s********\n" % downLoad.fileName
			downLoad.downloadFile()
	except:
		linkDownload(link).downloadFile()
	print
	print "FINISHED DOWNLOAD ALL FILE"
