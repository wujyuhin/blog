各种数据的描述[DataSet — EduData documentation](https://edudata.readthedocs.io/en/latest/tutorial/zh/DataSet.html)

EduData 的数据导入教程

```python
from EduData import get_data
import os

if not os.path.exists('../../data/anonymized_full_release_competition_dataset/anonymized_full_release_competition_dataset.csv'):
    get_data("assistment-2017", "../../data")
```

期中上述 `get_data` 函数需要输入想下载的数据名，和存放的路径

```
URL_DICT = {  
    "assistment-2009-2010-skill":  
        "http://base.ustc.edu.cn/data/ASSISTment/2009_skill_builder_data_corrected.zip",  
    "assistment-2012-2013-non-skill":  
        "http://base.ustc.edu.cn/data/ASSISTment/2012-2013-data-with-predictions-4-final.zip",  
    "assistment-2015":  
        "http://base.ustc.edu.cn/data/ASSISTment/2015_100_skill_builders_main_problems.zip",  
    "assistment-2017":  
        "http://base.ustc.edu.cn/data/ASSISTment/anonymized_full_release_competition_dataset.zip",  
    "junyi":  
        "http://base.ustc.edu.cn/data/JunyiAcademy_Math_Practicing_Log/junyi.rar",  
    "KDD-CUP-2010":  
        "http://base.ustc.edu.cn/data/KDD_Cup_2010/",  
    "NIPS-2020":  
        "http://base.ustc.edu.cn/data/NIPS2020/",  
    "slepemapy.cz":  
        "http://base.ustc.edu.cn/data/slepemapy.cz/",  
    "synthetic":  
        "http://base.ustc.edu.cn/data/synthetic/",  
    "psychometrics":  
        "http://base.ustc.edu.cn/data/psychometrics/",  
    "psy":  
        "http://base.ustc.edu.cn/data/psychometrics/",  
    "pisa2015":  
        "http://base.ustc.edu.cn/data/pisa2015_science.zip",  
    "workbankr":  
        "http://base.ustc.edu.cn/data/wordbankr.zip",  
    "critlangacq":  
        "http://base.ustc.edu.cn/data/critlangacq.zip",  
    "ktbd":  
        "http://base.ustc.edu.cn/data/ktbd/",  
    "ktbd-a0910":  
        "http://base.ustc.edu.cn/data/ktbd/assistment_2009_2010/",  
    "ktbd-junyi":  
        "http://base.ustc.edu.cn/data/ktbd/junyi/",  
    "ktbd-synthetic":  
        "http://base.ustc.edu.cn/data/ktbd/synthetic/",  
    "ktbd-a0910c":  
        "http://base.ustc.edu.cn/data/ktbd/a0910c/",  
    "cdbd":  
        "http://base.ustc.edu.cn/data/cdbd/",  
    "cdbd-lsat":  
        "http://base.ustc.edu.cn/data/cdbd/LSAT/",  
    "cdbd-a0910":  
        "http://base.ustc.edu.cn/data/cdbd/a0910/",  
    "math2015":  
        "http://staff.ustc.edu.cn/~qiliuql/data/math2015.rar",  
    "ednet":  
        "http://base.ustc.edu.cn/data/EdNet/",  
    "ktbd-ednet":  
        "http://base.ustc.edu.cn/data/ktbd/EdNet/",  
    "math23k":  
        "http://base.ustc.edu.cn/data/math23k.zip",  
    "OLI-Fall-2011":  
        "http://base.ustc.edu.cn/data/OLI_data.zip",  
    "open-luna":  
        "http://base.ustc.edu.cn/data/OpenLUNA/OpenLUNA.json"  
}
```