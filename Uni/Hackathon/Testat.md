stp programm angucken?
permissions?
1. chmod
2. 1. hidden feature?
3. 1. cheat sheet erlaubt
4. ipython3
5. 1. funktionen mit tab angezeigt; funktion? für infos
6. ![](../../Attachments/Pasted%20image%2020251030144815.png)


BEFEHLE
chmod 777  oder chmod +x
cp -r /opt/task2/ ./task2 ::::copy folder 



SCHRITT 2
def count_proc(path_to_file:str) -> str:
    lastid = ""
    DasIstEinTest456 = ""
    with open("/proc/cpuinfo", "r") as f:
        lines = f.readlines()
        for l in lines:
            if l.startswith("processor"):
                lastid = l.split(":")[1].strip()

    DasIstEinTest456 = int(lastid) + 1
    print(str(DasIstEinTest456) + " " + str(get_current_path()))
    return lastid



![](../../Attachments/Pasted%20image%2020251030195306.png)