filename = "kakaotalk_chat.txt"  #이곳에 카카오톡 대화 파일을 입력하세요

kt_file = open(filename,'r', encoding = 'utf8')      
kt_file_content = kt_file.readlines()   
kt_file.close()

#전처리
Kt_list = []
combined_sen =""

for i in kt_file_content:
    if('[오전' in i or '[오후' in i):  
        if(combined_sen!=""):    
            Kt_list.append(combined_sen)   
        combined_sen=i
    else:                
        combined_sen+=i   

Kt_list.append(combined_sen)  
del Kt_list[0]  

dict_text = {}   

while True:
    search = input()
    if (search == "\\laugh"): 
        for i in Kt_list:    
            if (i[0] == "["): 
                name = i[1:i.find("]")]  
            
            if ("ㅋ" in i or "ㅎ" in i): 
                if (name in dict_text):
                    dict_text[name] +=1
                else:
                    dict_text[name]=1  

    elif search == "\\cry":
        for i in Kt_list:
            if (i[0] == "["):
                name = i[1:i.find("]")]
            
            if ("ㅠ" in i or "ㅜ" in i):
                if (name in dict_text):
                    dict_text[name] +=1
                else:
                    dict_text[name]=1
    elif search == "\\swear":
        for i in Kt_list:
            if (i[0] == "["):
                name = i[1:i.find("]")]

            if ("ㅅㅂ" in i or "ㅗ" in i or "ㅈㄴ" in i or "꺼져" in i):  
                if (name in dict_text):
                    dict_text[name] +=1   
                else:
                    dict_text[name]=1 
    elif search == "\\talk":
        for i in Kt_list:
            if (i[0] == "["):
                name = i[1:i.find("]")]
                if (name in dict_text):
                    dict_text[name] +=1
                else:
                    dict_text[name]=1 
    elif search == "\\stop":
        print("입력이 끝났습니다.")
        break
    else: 
        for i in Kt_list:
            if (i[0] == "["):
                name= i[1:i.find("]")] 
            
            if (search in i): 
                if (name in dict_text):
                    dict_text[name] +=1
                else:
                    dict_text[name]=1 
    
    for i in range(len(dict_text)):  
        name=list(dict_text.keys())   
        number=list(dict_text.values())
        print(name[i]+':',number[i]) 
    dict_text.clear()   # -
카톡 대화 파일을 받아서 검색어를 입력하면 말한 사람과 그 횟수를 나타내는 코드입니다.
