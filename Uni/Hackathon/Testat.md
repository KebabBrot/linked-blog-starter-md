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

ipyhton3 hello.py cedoh001 - hier als input für sys.argv



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

dateien von einem verzeichnis in ein anderes kopieren

cp -a pfadzumverzeichnis/.         .





````python
import sys

# Einfach den vollständigen Pfad zum Ordner 'task3' hart codieren
task3_path = "/home/cedoh001/uebung/task3" # Passe diesen Pfad an!

if task3_path not in sys.path:
    sys.path.insert(0, task3_path)

import info_helper as ih
import count_and_publish as mud

def test_count_and_publish2():
    assert mud.count_proc("../cpuinfo/cpuinfo_2") == "2" + " " + str(ih.get_current_path())

def test_count_and_publish4():
    assert mud.count_proc("../cpuinfo/cpuinfo_4") == "4" + " " + str(ih.get_current_path())

def test_count_and_publish12():
    assert mud.count_proc("../cpuinfo/cpuinfo_12") == "12" + " " + str(ih.get_current_path())
```
