#爬取上海景点信息，去月销量最多的景点
import requests#导入第三方库requests
from openpyxl import workbook#写入Excel表所用
from bs4 import BeautifulSoup#导入python中BeautifulSoup库
#利用第三方库requests里的get方法爬取上海各景点信息,用while循环爬取多个网页信息，这里爬取3页上海各景点信息，并全部存入Z中
Z=[]
n=1
while n<10:
    r=requests.get('http://piao.qunar.com/ticket/list.htm?keyword=上海&region=&from=mpl_search_suggest&page='+str(n))
    if r.status_code==200:
        r.encoding = 'utf-8'
        html=r.text
        soup = BeautifulSoup(html,"html.parser")
        print(soup.prettify())
        #利用BeautifulSoup中find_all和select方法爬取各种信息
        #将景点所在区域存入A中
        A=[]
        for link in soup.find_all('span',class_="area"):
            A.append(link.get_text())
        #将各景点名称存入B中
        B=[]
        for link in soup.find_all('a',class_="name"):
            print(link.get_text())
            B.append(link.get_text())
        #将各景点票价存入C中
        C=[]
        for link in soup.select('span > em'):
            print(link.get_text())
            C.append(link.get_text())
        #将各景点票数的月销量存入D中
        D=[]
        for link in soup.find_all('span',class_="hot_num"):
            print(link.get_text())
            D.append(link.get_text())
        #将个景点的地址存入E中
        E=[]
        for link in soup.select('p > span'):
            print(link.get_text())
            E.append([link.get_text()[3:]])
        #对E中信息进行处理，删除无用信息
        E=E[0:15]
        #用while循环将各信息存入Z中
        k=0
        while k<15:
            Z.append([A[k][4:-1],B[k],C[k*2][3:],int(D[k]),E[k],C[k*2+1]])
            k=k+1
        print(Z)
        n=n+1
#对各景点信息按月销量进行排序（从高到低）
L=sorted(Z,key=lambda s:s[3],reverse=True)#用sorted方法排序
#将按月销量排好序的景点信息写入Excel文件中
global ws#全局工作表对象
wb = workbook.Workbook()#创建Excel对象
ws = wb.active#获取当前正在操作的表对象
#往表中写入标题行，以列表形式写入
ws.append(['所在区域','景点名称','热度','月销量','地址','价格'])
#用while循环将各景点信息写入
i=0
while i<(15*(n-1)):
    ws.append([L[i][0],L[i][1],float(L[i][2]),int(L[i][3]),L[i][4][0],float(L[i][5])])
    i=i+1
wb.save('Bignewtest.xlsx')#存入所有信息后，保存为test.xlsx