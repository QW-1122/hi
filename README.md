导入请求
从BS4导入美丽的汤
导入时间
导入随机

#=====这里改成你的小说URL=====
index_url="shturl.cc/PgnA1sBmlOKGZhkNmVWmA6yw"
save_name="逆仙伐神，从一只妖开始.文本"
#==============================

标头={
"用户代理"："Mozilla/5.0(Windows NT10.0；Win64；x64)AppleWebKit/537.36(KHTML，如Gecko)Chrome/120.0.0.0 Safari/537.36"
}

打印("===开始爬取===")
打印("1.正在获取目录页...")
res=requests.get(index_url，headers=headers)
res.encoding="utf-8"
print(f"状码：{res.status_code}")

soup=Beautiful Soup(res.text，"html.parser")

#找章节链接
打印("\n2.正在找章节链接...")
章节=[]
对于in soup.find_all("a")：
href=a.get("href"，"")
text=a.get_text(条带=True)
如果href.endswith(".html")和len(text)>2：
chapters.append((text，href))

标记(f"找到{len(章)}个章节")
如果Len(章节)>0：
打印("前3章预览：")
对于范围(3)中的i：
打印(f"{i+1}.{chapters[我][0]}->{章[我][1]}")

# 爬正文
打印("\n3.开始爬正文...")
将(save_name，"w"，encoding="utf-8")作为f打开：
对于枚举(chapters，1)中的i，(title，href)：
full_url=index_url.rstrip("/")+"/"+href
print(f"第{i}/{len(chapters)}章：{title}")
        
    尝试：
    R=请求。GET(full_url，headers=headers，timeout=10)
    r.encoding="utf-8"
    soup2=BeautifulSoup(r.text，"html.parser")
            
    #正文位置（适配piquge)
    content=soup2.find("div"，id="chaptercontent")
    如果没有内容：
    content=soup2.find("div"，class_="content")
            
    如果内容：
    text=content.get_text("\n"，条带=True)
    f.write(f"[{title}]\n{text}\n\n")
    print("✅成功保存")
    其他：
    打印("❌没找到正文")
    例外情况除外，如e：
    print(f"❌错误：{e}")
        
    time.sleep(random.uniform(1，2))

print(f"\n✅ 全部完成！文件已保存为：{保存名称}")

