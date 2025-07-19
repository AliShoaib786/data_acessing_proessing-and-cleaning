# data_acessing_proessing-and-cleaning
ais ma hum ne sub sy phly data ko gather kyh haa phr as ko clean kiyh haa 


# import numpy as  np
# import pandas as pd
# from fontTools.subset import subset
from unittest.mock import inplace

# ========================  duplication function on four dataset apply================

# patients=pd.read_csv('patients.csv')
# print("only patients \n ",patients[patients.duplicated(subset=['given_name','surname'])])

# treatment=pd.read_csv('treatments.csv')
# print("treatment \n",treatment[treatment.duplicated(subset=['given_name','surname'])])
#
# treatment_cut=pd.read_csv('treatments_cut.csv')
# print("treatment_cut \n",treatment_cut.duplicated().sum())

#
# advanture=pd.read_csv('adverse_reactions.csv')
# print("advanture \n",advanture.duplicated().sum())



# ====================   describe function =======================


# import numpy as  np
# import pandas as pd


# patients=pd.read_csv('patients.csv')
# print("only patients \n ",patients.describe())
#
# print(patients[patients['weight']==48.800000])



# ======================  treatment ======================

# treatment=pd.read_csv('treatments.csv')
# print("treatment \n",treatment.describe())
# print(treatment.sort_values('hba1c_change',na_position='first'))




# =================    completeness  first step oof claning thee data============

# import numpy as  np
# import pandas as pd
# from pandas.core.internals.construction import treat_as_nested

# ======================   completeness  first step to remove the missing value  in patient data set ===========
# patient=pd.read_csv('patients.csv')
# # print(patient.info())
# print(patient.fillna('no data',inplace=True))
# print(patient.info())



# =============  completeness  first step to remove the missing value  in treatment and treatment_cut data set=========

# treatment=pd.read_csv('treatments.csv')
# # print(treatment)
# print(treatment[treatment['hba1c_change'] == treatment['hba1c_start'] - treatment['hba1c_end']])
#
# print(treatment.info())


# ======================  concatenate  two table treatment and treatment_cut   that acessing and cleaning the process    =================
import numpy as  np
import pandas as pd
from pandas.core.internals.construction import treat_as_nested

treatment=pd.read_csv('treatments.csv')
print(treatment)
treatment_cut=pd.read_csv('treatments_cut.csv')
print(treatment_cut)
concate=pd.concat([treatment,treatment_cut])
print(concate)


full=concate.melt(id_vars=['given_name','surname','auralin','hba1c_start','hba1c_end','hba1c_change'],var_name='type',value_name='dosage_range')
print(full[full['dosage_range']!="_"])
# ======================  'dosage_range start'  aur  'dosage_range end ' ki values ko  alada aladah colum ko store
# =================   kary ga
full['dosage_range start']=full['dosage_range'].str.split('-').str.get(0)
full['dosage_range end']=full['dosage_range'].str.split('-').str.get(1)
print(full['dosage_range start'])
print(full['dosage_range end'])
print(full.drop(columns='dosage_range',inplace=True))

# =============  yeh code joo haa voo dosage_range start or dosage_range end  ma sy 'u' ki value ko katam kr dy ga
full['dosage_range start']=full['dosage_range start'].str.replace('u','')
full['dosage_range end']=full['dosage_range end'].str.replace('u','')


# ================  dosage_range starrt  and dosage_range end  ain ka data type joo haa object show horah haa ain ko hum ne
#   integer ma tabdel krna haa

full['dosage_range start']=full['dosage_range start'].astype('int32')
full['dosage_range end']=full['dosage_range end'].astype('int32')
print(full)
print(full.info())

