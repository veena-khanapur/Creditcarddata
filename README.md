# Creditcarddata
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 1,
   "id": "46d6ffb3",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Importing the Libraries\n",
    "import numpy as np\n",
    "import pandas as pd\n",
    "from sklearn.model_selection import train_test_split\n",
    "from sklearn.linear_model import LogisticRegression\n",
    "from sklearn.ensemble import RandomForestClassifier\n",
    "from sklearn.metrics import accuracy_score\n",
    "import matplotlib.pyplot as plt\n",
    "from matplotlib import gridspec\n",
    "from sklearn.metrics import precision_score,recall_score,f1_score\n",
    "from sklearn.tree import DecisionTreeClassifier\n",
    "import seaborn as sns\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "id": "629c5197",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Load the Dataset to Pandas dataframe\n",
    "credit_card_data = pd.read_csv('creditcard.csv')"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "id": "2323a610",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "      <th>Class</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>0.0</td>\n",
       "      <td>-1.359807</td>\n",
       "      <td>-0.072781</td>\n",
       "      <td>2.536347</td>\n",
       "      <td>1.378155</td>\n",
       "      <td>-0.338321</td>\n",
       "      <td>0.462388</td>\n",
       "      <td>0.239599</td>\n",
       "      <td>0.098698</td>\n",
       "      <td>0.363787</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.018307</td>\n",
       "      <td>0.277838</td>\n",
       "      <td>-0.110474</td>\n",
       "      <td>0.066928</td>\n",
       "      <td>0.128539</td>\n",
       "      <td>-0.189115</td>\n",
       "      <td>0.133558</td>\n",
       "      <td>-0.021053</td>\n",
       "      <td>149.62</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>0.0</td>\n",
       "      <td>1.191857</td>\n",
       "      <td>0.266151</td>\n",
       "      <td>0.166480</td>\n",
       "      <td>0.448154</td>\n",
       "      <td>0.060018</td>\n",
       "      <td>-0.082361</td>\n",
       "      <td>-0.078803</td>\n",
       "      <td>0.085102</td>\n",
       "      <td>-0.255425</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.225775</td>\n",
       "      <td>-0.638672</td>\n",
       "      <td>0.101288</td>\n",
       "      <td>-0.339846</td>\n",
       "      <td>0.167170</td>\n",
       "      <td>0.125895</td>\n",
       "      <td>-0.008983</td>\n",
       "      <td>0.014724</td>\n",
       "      <td>2.69</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-1.358354</td>\n",
       "      <td>-1.340163</td>\n",
       "      <td>1.773209</td>\n",
       "      <td>0.379780</td>\n",
       "      <td>-0.503198</td>\n",
       "      <td>1.800499</td>\n",
       "      <td>0.791461</td>\n",
       "      <td>0.247676</td>\n",
       "      <td>-1.514654</td>\n",
       "      <td>...</td>\n",
       "      <td>0.247998</td>\n",
       "      <td>0.771679</td>\n",
       "      <td>0.909412</td>\n",
       "      <td>-0.689281</td>\n",
       "      <td>-0.327642</td>\n",
       "      <td>-0.139097</td>\n",
       "      <td>-0.055353</td>\n",
       "      <td>-0.059752</td>\n",
       "      <td>378.66</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>1.0</td>\n",
       "      <td>-0.966272</td>\n",
       "      <td>-0.185226</td>\n",
       "      <td>1.792993</td>\n",
       "      <td>-0.863291</td>\n",
       "      <td>-0.010309</td>\n",
       "      <td>1.247203</td>\n",
       "      <td>0.237609</td>\n",
       "      <td>0.377436</td>\n",
       "      <td>-1.387024</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.108300</td>\n",
       "      <td>0.005274</td>\n",
       "      <td>-0.190321</td>\n",
       "      <td>-1.175575</td>\n",
       "      <td>0.647376</td>\n",
       "      <td>-0.221929</td>\n",
       "      <td>0.062723</td>\n",
       "      <td>0.061458</td>\n",
       "      <td>123.50</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>2.0</td>\n",
       "      <td>-1.158233</td>\n",
       "      <td>0.877737</td>\n",
       "      <td>1.548718</td>\n",
       "      <td>0.403034</td>\n",
       "      <td>-0.407193</td>\n",
       "      <td>0.095921</td>\n",
       "      <td>0.592941</td>\n",
       "      <td>-0.270533</td>\n",
       "      <td>0.817739</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.009431</td>\n",
       "      <td>0.798278</td>\n",
       "      <td>-0.137458</td>\n",
       "      <td>0.141267</td>\n",
       "      <td>-0.206010</td>\n",
       "      <td>0.502292</td>\n",
       "      <td>0.219422</td>\n",
       "      <td>0.215153</td>\n",
       "      <td>69.99</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 31 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "   Time        V1        V2        V3        V4        V5        V6        V7  \\\n",
       "0   0.0 -1.359807 -0.072781  2.536347  1.378155 -0.338321  0.462388  0.239599   \n",
       "1   0.0  1.191857  0.266151  0.166480  0.448154  0.060018 -0.082361 -0.078803   \n",
       "2   1.0 -1.358354 -1.340163  1.773209  0.379780 -0.503198  1.800499  0.791461   \n",
       "3   1.0 -0.966272 -0.185226  1.792993 -0.863291 -0.010309  1.247203  0.237609   \n",
       "4   2.0 -1.158233  0.877737  1.548718  0.403034 -0.407193  0.095921  0.592941   \n",
       "\n",
       "         V8        V9  ...       V21       V22       V23       V24       V25  \\\n",
       "0  0.098698  0.363787  ... -0.018307  0.277838 -0.110474  0.066928  0.128539   \n",
       "1  0.085102 -0.255425  ... -0.225775 -0.638672  0.101288 -0.339846  0.167170   \n",
       "2  0.247676 -1.514654  ...  0.247998  0.771679  0.909412 -0.689281 -0.327642   \n",
       "3  0.377436 -1.387024  ... -0.108300  0.005274 -0.190321 -1.175575  0.647376   \n",
       "4 -0.270533  0.817739  ... -0.009431  0.798278 -0.137458  0.141267 -0.206010   \n",
       "\n",
       "        V26       V27       V28  Amount  Class  \n",
       "0 -0.189115  0.133558 -0.021053  149.62      0  \n",
       "1  0.125895 -0.008983  0.014724    2.69      0  \n",
       "2 -0.139097 -0.055353 -0.059752  378.66      0  \n",
       "3 -0.221929  0.062723  0.061458  123.50      0  \n",
       "4  0.502292  0.219422  0.215153   69.99      0  \n",
       "\n",
       "[5 rows x 31 columns]"
      ]
     },
     "execution_count": 3,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Showing 5 rows the dataset\n",
    "credit_card_data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "id": "5c95c6b1",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "      <th>Class</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>284802</th>\n",
       "      <td>172786.0</td>\n",
       "      <td>-11.881118</td>\n",
       "      <td>10.071785</td>\n",
       "      <td>-9.834783</td>\n",
       "      <td>-2.066656</td>\n",
       "      <td>-5.364473</td>\n",
       "      <td>-2.606837</td>\n",
       "      <td>-4.918215</td>\n",
       "      <td>7.305334</td>\n",
       "      <td>1.914428</td>\n",
       "      <td>...</td>\n",
       "      <td>0.213454</td>\n",
       "      <td>0.111864</td>\n",
       "      <td>1.014480</td>\n",
       "      <td>-0.509348</td>\n",
       "      <td>1.436807</td>\n",
       "      <td>0.250034</td>\n",
       "      <td>0.943651</td>\n",
       "      <td>0.823731</td>\n",
       "      <td>0.77</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>284803</th>\n",
       "      <td>172787.0</td>\n",
       "      <td>-0.732789</td>\n",
       "      <td>-0.055080</td>\n",
       "      <td>2.035030</td>\n",
       "      <td>-0.738589</td>\n",
       "      <td>0.868229</td>\n",
       "      <td>1.058415</td>\n",
       "      <td>0.024330</td>\n",
       "      <td>0.294869</td>\n",
       "      <td>0.584800</td>\n",
       "      <td>...</td>\n",
       "      <td>0.214205</td>\n",
       "      <td>0.924384</td>\n",
       "      <td>0.012463</td>\n",
       "      <td>-1.016226</td>\n",
       "      <td>-0.606624</td>\n",
       "      <td>-0.395255</td>\n",
       "      <td>0.068472</td>\n",
       "      <td>-0.053527</td>\n",
       "      <td>24.79</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>284804</th>\n",
       "      <td>172788.0</td>\n",
       "      <td>1.919565</td>\n",
       "      <td>-0.301254</td>\n",
       "      <td>-3.249640</td>\n",
       "      <td>-0.557828</td>\n",
       "      <td>2.630515</td>\n",
       "      <td>3.031260</td>\n",
       "      <td>-0.296827</td>\n",
       "      <td>0.708417</td>\n",
       "      <td>0.432454</td>\n",
       "      <td>...</td>\n",
       "      <td>0.232045</td>\n",
       "      <td>0.578229</td>\n",
       "      <td>-0.037501</td>\n",
       "      <td>0.640134</td>\n",
       "      <td>0.265745</td>\n",
       "      <td>-0.087371</td>\n",
       "      <td>0.004455</td>\n",
       "      <td>-0.026561</td>\n",
       "      <td>67.88</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>284805</th>\n",
       "      <td>172788.0</td>\n",
       "      <td>-0.240440</td>\n",
       "      <td>0.530483</td>\n",
       "      <td>0.702510</td>\n",
       "      <td>0.689799</td>\n",
       "      <td>-0.377961</td>\n",
       "      <td>0.623708</td>\n",
       "      <td>-0.686180</td>\n",
       "      <td>0.679145</td>\n",
       "      <td>0.392087</td>\n",
       "      <td>...</td>\n",
       "      <td>0.265245</td>\n",
       "      <td>0.800049</td>\n",
       "      <td>-0.163298</td>\n",
       "      <td>0.123205</td>\n",
       "      <td>-0.569159</td>\n",
       "      <td>0.546668</td>\n",
       "      <td>0.108821</td>\n",
       "      <td>0.104533</td>\n",
       "      <td>10.00</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>284806</th>\n",
       "      <td>172792.0</td>\n",
       "      <td>-0.533413</td>\n",
       "      <td>-0.189733</td>\n",
       "      <td>0.703337</td>\n",
       "      <td>-0.506271</td>\n",
       "      <td>-0.012546</td>\n",
       "      <td>-0.649617</td>\n",
       "      <td>1.577006</td>\n",
       "      <td>-0.414650</td>\n",
       "      <td>0.486180</td>\n",
       "      <td>...</td>\n",
       "      <td>0.261057</td>\n",
       "      <td>0.643078</td>\n",
       "      <td>0.376777</td>\n",
       "      <td>0.008797</td>\n",
       "      <td>-0.473649</td>\n",
       "      <td>-0.818267</td>\n",
       "      <td>-0.002415</td>\n",
       "      <td>0.013649</td>\n",
       "      <td>217.00</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 31 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "            Time         V1         V2        V3        V4        V5  \\\n",
       "284802  172786.0 -11.881118  10.071785 -9.834783 -2.066656 -5.364473   \n",
       "284803  172787.0  -0.732789  -0.055080  2.035030 -0.738589  0.868229   \n",
       "284804  172788.0   1.919565  -0.301254 -3.249640 -0.557828  2.630515   \n",
       "284805  172788.0  -0.240440   0.530483  0.702510  0.689799 -0.377961   \n",
       "284806  172792.0  -0.533413  -0.189733  0.703337 -0.506271 -0.012546   \n",
       "\n",
       "              V6        V7        V8        V9  ...       V21       V22  \\\n",
       "284802 -2.606837 -4.918215  7.305334  1.914428  ...  0.213454  0.111864   \n",
       "284803  1.058415  0.024330  0.294869  0.584800  ...  0.214205  0.924384   \n",
       "284804  3.031260 -0.296827  0.708417  0.432454  ...  0.232045  0.578229   \n",
       "284805  0.623708 -0.686180  0.679145  0.392087  ...  0.265245  0.800049   \n",
       "284806 -0.649617  1.577006 -0.414650  0.486180  ...  0.261057  0.643078   \n",
       "\n",
       "             V23       V24       V25       V26       V27       V28  Amount  \\\n",
       "284802  1.014480 -0.509348  1.436807  0.250034  0.943651  0.823731    0.77   \n",
       "284803  0.012463 -1.016226 -0.606624 -0.395255  0.068472 -0.053527   24.79   \n",
       "284804 -0.037501  0.640134  0.265745 -0.087371  0.004455 -0.026561   67.88   \n",
       "284805 -0.163298  0.123205 -0.569159  0.546668  0.108821  0.104533   10.00   \n",
       "284806  0.376777  0.008797 -0.473649 -0.818267 -0.002415  0.013649  217.00   \n",
       "\n",
       "        Class  \n",
       "284802      0  \n",
       "284803      0  \n",
       "284804      0  \n",
       "284805      0  \n",
       "284806      0  \n",
       "\n",
       "[5 rows x 31 columns]"
      ]
     },
     "execution_count": 4,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "\n",
    "credit_card_data.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "id": "56595e07",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "<class 'pandas.core.frame.DataFrame'>\n",
      "RangeIndex: 284807 entries, 0 to 284806\n",
      "Data columns (total 31 columns):\n",
      " #   Column  Non-Null Count   Dtype  \n",
      "---  ------  --------------   -----  \n",
      " 0   Time    284807 non-null  float64\n",
      " 1   V1      284807 non-null  float64\n",
      " 2   V2      284807 non-null  float64\n",
      " 3   V3      284807 non-null  float64\n",
      " 4   V4      284807 non-null  float64\n",
      " 5   V5      284807 non-null  float64\n",
      " 6   V6      284807 non-null  float64\n",
      " 7   V7      284807 non-null  float64\n",
      " 8   V8      284807 non-null  float64\n",
      " 9   V9      284807 non-null  float64\n",
      " 10  V10     284807 non-null  float64\n",
      " 11  V11     284807 non-null  float64\n",
      " 12  V12     284807 non-null  float64\n",
      " 13  V13     284807 non-null  float64\n",
      " 14  V14     284807 non-null  float64\n",
      " 15  V15     284807 non-null  float64\n",
      " 16  V16     284807 non-null  float64\n",
      " 17  V17     284807 non-null  float64\n",
      " 18  V18     284807 non-null  float64\n",
      " 19  V19     284807 non-null  float64\n",
      " 20  V20     284807 non-null  float64\n",
      " 21  V21     284807 non-null  float64\n",
      " 22  V22     284807 non-null  float64\n",
      " 23  V23     284807 non-null  float64\n",
      " 24  V24     284807 non-null  float64\n",
      " 25  V25     284807 non-null  float64\n",
      " 26  V26     284807 non-null  float64\n",
      " 27  V27     284807 non-null  float64\n",
      " 28  V28     284807 non-null  float64\n",
      " 29  Amount  284807 non-null  float64\n",
      " 30  Class   284807 non-null  int64  \n",
      "dtypes: float64(30), int64(1)\n",
      "memory usage: 67.4 MB\n"
     ]
    }
   ],
   "source": [
    "# Information of Dataset\n",
    "credit_card_data.info()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "id": "c790bcdc",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Time      0\n",
       "V1        0\n",
       "V2        0\n",
       "V3        0\n",
       "V4        0\n",
       "V5        0\n",
       "V6        0\n",
       "V7        0\n",
       "V8        0\n",
       "V9        0\n",
       "V10       0\n",
       "V11       0\n",
       "V12       0\n",
       "V13       0\n",
       "V14       0\n",
       "V15       0\n",
       "V16       0\n",
       "V17       0\n",
       "V18       0\n",
       "V19       0\n",
       "V20       0\n",
       "V21       0\n",
       "V22       0\n",
       "V23       0\n",
       "V24       0\n",
       "V25       0\n",
       "V26       0\n",
       "V27       0\n",
       "V28       0\n",
       "Amount    0\n",
       "Class     0\n",
       "dtype: int64"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Check Missing Values for each column\n",
    "credit_card_data.isnull().sum()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "id": "781831b8",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Class\n",
       "0    284315\n",
       "1       492\n",
       "Name: count, dtype: int64"
      ]
     },
     "execution_count": 7,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "# Distribution of Legit and Fraudulent transctions\n",
    "credit_card_data['Class'].value_counts()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "id": "70879d35",
   "metadata": {},
   "outputs": [],
   "source": [
    "# The Dataset is Unbalanced where 99% of data is legit\n",
    "#Label 0 -- Normal transaction\n",
    "#Label 1 -- Fraudulent transaction"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "id": "695aeb8d",
   "metadata": {},
   "outputs": [],
   "source": [
    "# Breaking the data for analysis\n",
    "legit = credit_card_data[credit_card_data.Class == 0]\n",
    "fraud = credit_card_data[credit_card_data.Class == 1]"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "id": "a6a17b2c",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(284315, 31)\n",
      "(492, 31)\n",
      "Proportion of Fraudulent Cases: 0.001727485630620034\n"
     ]
    }
   ],
   "source": [
    "#print(\"Proportion of Fraudulent Cases: \" + str(len(dataset[dataset[\"Class\"] == 1])/ dataset.shape[0]))\n",
    "# The shape of legit and fraud transactions\n",
    "print(legit.shape)\n",
    "print(fraud.shape)\n",
    "print(\"Proportion of Fraudulent Cases: \" + str(len(credit_card_data[credit_card_data[\"Class\"] == 1])/ credit_card_data.shape[0]))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "id": "a8f6a001",
   "metadata": {},
   "outputs": [],
   "source": [
    "# To see fraud transcations vs overall transactions\n",
    "data_p = credit_card_data.copy()\n",
    "data_p[\" \"] = np.where(data_p[\"Class\"] == 1 ,  \"fraud\", \"legit\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "id": "80154f85",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<Axes: ylabel='count'>"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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cjDh02m9HTt2nPJt+/btJ9y/pqZGEydOVJs2bZSYmKihQ4dq0aJFx9zn5ZdfVrt27ZSQkKCrr75aU6dOVbNmzeo/f/RpvUmTJmnGjBn66KOP6lesOP7xGssVpnO3AIQ+dxNfPM+dO1dvvPGGPv74Y+Xm5qpPnz5+ShY4Ps9zaozbb79dO3fu1D/+8Q+1bt1as2fP1mWXXaa1a9eqW7duWrp0qe655x49/fTTuuKKK/TZZ5/pN7/5zSkfb8KECdqwYYNKSkr0+uuvS5JatGjRpIxccwJgV0198bxt2za1atVK55577kk/X1NTo5iYmCZ9DX/zqZzuuOOO037+tddeq39/27Zteuedd7R37161bt1aUl25zJ07V6+//romT56s6dOn6/LLL9eECRMkSdnZ2friiy/08ccfn/Txk5KSFB8fr+rqamVlZfnyTzhBUw+bASBQmnLN6bbbbtOMGTMk1V126dChgzp27Kg+ffooJiZGM2fOVO/evbV48WJNnTpVr7/+urZv364WLVpozJgxeuaZZ+ovqUyaNEkffvihVq1aVf/406ZN07Rp07Rz5866rG63HnroIb322mtyOp2688475fVhi3Gfh5If/VZQUKAFCxbogw8+OGGfp5UrV8rr9So7O7v+utGR61Xbtm2TJG3atElDhgw55u8d/3GgReIFRwChoSnXxP/85z/r97//vdq2bavc3Fx98803kqQZM2YoKipKS5cu1YsvvihJcjgceu6557Ru3TrNmDFDCxYs0MSJExv19aZMmaLXXntNr776qpYsWaLCwkLNnj270bl9OnI62RfyeDz62c9+ps6dO59wu9Pp1IoVK05YFPZIG3u93mNWmThyWzAd9+WBJnNaHsU4vIqyvIq2vIpySNGWR9GWV9EOr5yHb492eBVleRRleY978xx+q3usaMsrp+WRU15FObyKPvy+Ux5FOQ7/adX96bC8ipKn/v71t1keOVX35lBdBoeOvc1x+O85vB455ZbD8srh9cihI2/ew3+65fB6ZB25zeuWQx5ZXo8seeWQW5bXI4fXLUseWV6vrPr7uGV5vdLh23F6DusVSSk+/d3U1FQlJyfL6XQec6apa9eueuaZZ46579HTfzp16qTHH39c9957r55//vkGf71p06bpkUce0bXXXitJeuGFF/TJJ580Orffrjk5HA498MADGjFi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",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "# plot a pie chart for the same\n",
    "data_p[\" \"].value_counts().plot(kind=\"pie\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "id": "22912137",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count    284315.000000\n",
       "mean         88.291022\n",
       "std         250.105092\n",
       "min           0.000000\n",
       "25%           5.650000\n",
       "50%          22.000000\n",
       "75%          77.050000\n",
       "max       25691.160000\n",
       "Name: Amount, dtype: float64"
      ]
     },
     "execution_count": 13,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#statistical maesure of the data for legit and fraud\n",
    "legit.Amount.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "id": "3b58ad1c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "count     492.000000\n",
       "mean      122.211321\n",
       "std       256.683288\n",
       "min         0.000000\n",
       "25%         1.000000\n",
       "50%         9.250000\n",
       "75%       105.890000\n",
       "max      2125.870000\n",
       "Name: Amount, dtype: float64"
      ]
     },
     "execution_count": 14,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "fraud.Amount.describe()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "id": "8bee9cab",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V20</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Class</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>94838.202258</td>\n",
       "      <td>0.008258</td>\n",
       "      <td>-0.006271</td>\n",
       "      <td>0.012171</td>\n",
       "      <td>-0.007860</td>\n",
       "      <td>0.005453</td>\n",
       "      <td>0.002419</td>\n",
       "      <td>0.009637</td>\n",
       "      <td>-0.000987</td>\n",
       "      <td>0.004467</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.000644</td>\n",
       "      <td>-0.001235</td>\n",
       "      <td>-0.000024</td>\n",
       "      <td>0.000070</td>\n",
       "      <td>0.000182</td>\n",
       "      <td>-0.000072</td>\n",
       "      <td>-0.000089</td>\n",
       "      <td>-0.000295</td>\n",
       "      <td>-0.000131</td>\n",
       "      <td>88.291022</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>80746.806911</td>\n",
       "      <td>-4.771948</td>\n",
       "      <td>3.623778</td>\n",
       "      <td>-7.033281</td>\n",
       "      <td>4.542029</td>\n",
       "      <td>-3.151225</td>\n",
       "      <td>-1.397737</td>\n",
       "      <td>-5.568731</td>\n",
       "      <td>0.570636</td>\n",
       "      <td>-2.581123</td>\n",
       "      <td>...</td>\n",
       "      <td>0.372319</td>\n",
       "      <td>0.713588</td>\n",
       "      <td>0.014049</td>\n",
       "      <td>-0.040308</td>\n",
       "      <td>-0.105130</td>\n",
       "      <td>0.041449</td>\n",
       "      <td>0.051648</td>\n",
       "      <td>0.170575</td>\n",
       "      <td>0.075667</td>\n",
       "      <td>122.211321</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 30 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "               Time        V1        V2        V3        V4        V5  \\\n",
       "Class                                                                   \n",
       "0      94838.202258  0.008258 -0.006271  0.012171 -0.007860  0.005453   \n",
       "1      80746.806911 -4.771948  3.623778 -7.033281  4.542029 -3.151225   \n",
       "\n",
       "             V6        V7        V8        V9  ...       V20       V21  \\\n",
       "Class                                          ...                       \n",
       "0      0.002419  0.009637 -0.000987  0.004467  ... -0.000644 -0.001235   \n",
       "1     -1.397737 -5.568731  0.570636 -2.581123  ...  0.372319  0.713588   \n",
       "\n",
       "            V22       V23       V24       V25       V26       V27       V28  \\\n",
       "Class                                                                         \n",
       "0     -0.000024  0.000070  0.000182 -0.000072 -0.000089 -0.000295 -0.000131   \n",
       "1      0.014049 -0.040308 -0.105130  0.041449  0.051648  0.170575  0.075667   \n",
       "\n",
       "           Amount  \n",
       "Class              \n",
       "0       88.291022  \n",
       "1      122.211321  \n",
       "\n",
       "[2 rows x 30 columns]"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Compare Values of both transaction\n",
    "credit_card_data.groupby('Class').mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "id": "306e93a2",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Building a sample dataset  out of given dataset\n",
    "# Number of fraudulent transaction is 492 so taking sample of 492 legit transactions\n",
    "legit_sample = legit.sample(n=492)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "id": "f09fb567",
   "metadata": {},
   "outputs": [],
   "source": [
    "#joining the legit sample 492 transactions and fraudulent 492 transactions using concate function\n",
    "new_dataset = pd.concat([legit_sample,fraud],axis=0)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 18,
   "id": "d4ed8810",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "      <th>Class</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>177198</th>\n",
       "      <td>123080.0</td>\n",
       "      <td>1.973186</td>\n",
       "      <td>-0.641150</td>\n",
       "      <td>-0.542609</td>\n",
       "      <td>0.341897</td>\n",
       "      <td>-0.577897</td>\n",
       "      <td>0.050004</td>\n",
       "      <td>-0.806373</td>\n",
       "      <td>0.161339</td>\n",
       "      <td>1.496749</td>\n",
       "      <td>...</td>\n",
       "      <td>0.135113</td>\n",
       "      <td>0.468296</td>\n",
       "      <td>0.169180</td>\n",
       "      <td>0.431069</td>\n",
       "      <td>-0.292862</td>\n",
       "      <td>0.560037</td>\n",
       "      <td>-0.034632</td>\n",
       "      <td>-0.043273</td>\n",
       "      <td>28.75</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>151075</th>\n",
       "      <td>94537.0</td>\n",
       "      <td>1.719386</td>\n",
       "      <td>0.402091</td>\n",
       "      <td>-0.899124</td>\n",
       "      <td>3.611173</td>\n",
       "      <td>1.257730</td>\n",
       "      <td>1.579898</td>\n",
       "      <td>-0.086648</td>\n",
       "      <td>0.311985</td>\n",
       "      <td>-0.045239</td>\n",
       "      <td>...</td>\n",
       "      <td>0.215670</td>\n",
       "      <td>0.854776</td>\n",
       "      <td>0.084477</td>\n",
       "      <td>-1.450250</td>\n",
       "      <td>-0.143424</td>\n",
       "      <td>0.188958</td>\n",
       "      <td>-0.033348</td>\n",
       "      <td>-0.077165</td>\n",
       "      <td>43.24</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>177683</th>\n",
       "      <td>123290.0</td>\n",
       "      <td>-5.439683</td>\n",
       "      <td>-4.147777</td>\n",
       "      <td>-5.959422</td>\n",
       "      <td>-0.887167</td>\n",
       "      <td>-13.689013</td>\n",
       "      <td>7.845434</td>\n",
       "      <td>12.571331</td>\n",
       "      <td>-1.169319</td>\n",
       "      <td>-1.840041</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.997839</td>\n",
       "      <td>-0.028644</td>\n",
       "      <td>1.875669</td>\n",
       "      <td>0.590515</td>\n",
       "      <td>-0.456819</td>\n",
       "      <td>-0.687225</td>\n",
       "      <td>2.529994</td>\n",
       "      <td>-2.177994</td>\n",
       "      <td>3017.28</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>85531</th>\n",
       "      <td>60808.0</td>\n",
       "      <td>-3.940556</td>\n",
       "      <td>-3.915472</td>\n",
       "      <td>1.895930</td>\n",
       "      <td>0.716928</td>\n",
       "      <td>3.982146</td>\n",
       "      <td>-3.180268</td>\n",
       "      <td>-1.881820</td>\n",
       "      <td>-0.178257</td>\n",
       "      <td>0.954933</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.396018</td>\n",
       "      <td>-0.429042</td>\n",
       "      <td>-0.578267</td>\n",
       "      <td>0.637504</td>\n",
       "      <td>-0.348859</td>\n",
       "      <td>0.012972</td>\n",
       "      <td>0.379042</td>\n",
       "      <td>-0.380173</td>\n",
       "      <td>78.41</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>188135</th>\n",
       "      <td>127833.0</td>\n",
       "      <td>-1.606631</td>\n",
       "      <td>-0.832683</td>\n",
       "      <td>0.255481</td>\n",
       "      <td>-0.601391</td>\n",
       "      <td>2.788026</td>\n",
       "      <td>-1.748567</td>\n",
       "      <td>-0.122949</td>\n",
       "      <td>0.152840</td>\n",
       "      <td>-0.428752</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.066507</td>\n",
       "      <td>-0.782261</td>\n",
       "      <td>0.300438</td>\n",
       "      <td>0.651297</td>\n",
       "      <td>-0.375981</td>\n",
       "      <td>0.001595</td>\n",
       "      <td>0.009563</td>\n",
       "      <td>0.207905</td>\n",
       "      <td>1.98</td>\n",
       "      <td>0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 31 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "            Time        V1        V2        V3        V4         V5        V6  \\\n",
       "177198  123080.0  1.973186 -0.641150 -0.542609  0.341897  -0.577897  0.050004   \n",
       "151075   94537.0  1.719386  0.402091 -0.899124  3.611173   1.257730  1.579898   \n",
       "177683  123290.0 -5.439683 -4.147777 -5.959422 -0.887167 -13.689013  7.845434   \n",
       "85531    60808.0 -3.940556 -3.915472  1.895930  0.716928   3.982146 -3.180268   \n",
       "188135  127833.0 -1.606631 -0.832683  0.255481 -0.601391   2.788026 -1.748567   \n",
       "\n",
       "               V7        V8        V9  ...       V21       V22       V23  \\\n",
       "177198  -0.806373  0.161339  1.496749  ...  0.135113  0.468296  0.169180   \n",
       "151075  -0.086648  0.311985 -0.045239  ...  0.215670  0.854776  0.084477   \n",
       "177683  12.571331 -1.169319 -1.840041  ... -0.997839 -0.028644  1.875669   \n",
       "85531   -1.881820 -0.178257  0.954933  ... -0.396018 -0.429042 -0.578267   \n",
       "188135  -0.122949  0.152840 -0.428752  ... -0.066507 -0.782261  0.300438   \n",
       "\n",
       "             V24       V25       V26       V27       V28   Amount  Class  \n",
       "177198  0.431069 -0.292862  0.560037 -0.034632 -0.043273    28.75      0  \n",
       "151075 -1.450250 -0.143424  0.188958 -0.033348 -0.077165    43.24      0  \n",
       "177683  0.590515 -0.456819 -0.687225  2.529994 -2.177994  3017.28      0  \n",
       "85531   0.637504 -0.348859  0.012972  0.379042 -0.380173    78.41      0  \n",
       "188135  0.651297 -0.375981  0.001595  0.009563  0.207905     1.98      0  \n",
       "\n",
       "[5 rows x 31 columns]"
      ]
     },
     "execution_count": 18,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#checking the joined new dataset with top 5rows and last 5 rows\n",
    "new_dataset.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 19,
   "id": "0efe2483",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "      <th>Class</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>279863</th>\n",
       "      <td>169142.0</td>\n",
       "      <td>-1.927883</td>\n",
       "      <td>1.125653</td>\n",
       "      <td>-4.518331</td>\n",
       "      <td>1.749293</td>\n",
       "      <td>-1.566487</td>\n",
       "      <td>-2.010494</td>\n",
       "      <td>-0.882850</td>\n",
       "      <td>0.697211</td>\n",
       "      <td>-2.064945</td>\n",
       "      <td>...</td>\n",
       "      <td>0.778584</td>\n",
       "      <td>-0.319189</td>\n",
       "      <td>0.639419</td>\n",
       "      <td>-0.294885</td>\n",
       "      <td>0.537503</td>\n",
       "      <td>0.788395</td>\n",
       "      <td>0.292680</td>\n",
       "      <td>0.147968</td>\n",
       "      <td>390.00</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>280143</th>\n",
       "      <td>169347.0</td>\n",
       "      <td>1.378559</td>\n",
       "      <td>1.289381</td>\n",
       "      <td>-5.004247</td>\n",
       "      <td>1.411850</td>\n",
       "      <td>0.442581</td>\n",
       "      <td>-1.326536</td>\n",
       "      <td>-1.413170</td>\n",
       "      <td>0.248525</td>\n",
       "      <td>-1.127396</td>\n",
       "      <td>...</td>\n",
       "      <td>0.370612</td>\n",
       "      <td>0.028234</td>\n",
       "      <td>-0.145640</td>\n",
       "      <td>-0.081049</td>\n",
       "      <td>0.521875</td>\n",
       "      <td>0.739467</td>\n",
       "      <td>0.389152</td>\n",
       "      <td>0.186637</td>\n",
       "      <td>0.76</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>280149</th>\n",
       "      <td>169351.0</td>\n",
       "      <td>-0.676143</td>\n",
       "      <td>1.126366</td>\n",
       "      <td>-2.213700</td>\n",
       "      <td>0.468308</td>\n",
       "      <td>-1.120541</td>\n",
       "      <td>-0.003346</td>\n",
       "      <td>-2.234739</td>\n",
       "      <td>1.210158</td>\n",
       "      <td>-0.652250</td>\n",
       "      <td>...</td>\n",
       "      <td>0.751826</td>\n",
       "      <td>0.834108</td>\n",
       "      <td>0.190944</td>\n",
       "      <td>0.032070</td>\n",
       "      <td>-0.739695</td>\n",
       "      <td>0.471111</td>\n",
       "      <td>0.385107</td>\n",
       "      <td>0.194361</td>\n",
       "      <td>77.89</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>281144</th>\n",
       "      <td>169966.0</td>\n",
       "      <td>-3.113832</td>\n",
       "      <td>0.585864</td>\n",
       "      <td>-5.399730</td>\n",
       "      <td>1.817092</td>\n",
       "      <td>-0.840618</td>\n",
       "      <td>-2.943548</td>\n",
       "      <td>-2.208002</td>\n",
       "      <td>1.058733</td>\n",
       "      <td>-1.632333</td>\n",
       "      <td>...</td>\n",
       "      <td>0.583276</td>\n",
       "      <td>-0.269209</td>\n",
       "      <td>-0.456108</td>\n",
       "      <td>-0.183659</td>\n",
       "      <td>-0.328168</td>\n",
       "      <td>0.606116</td>\n",
       "      <td>0.884876</td>\n",
       "      <td>-0.253700</td>\n",
       "      <td>245.00</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>281674</th>\n",
       "      <td>170348.0</td>\n",
       "      <td>1.991976</td>\n",
       "      <td>0.158476</td>\n",
       "      <td>-2.583441</td>\n",
       "      <td>0.408670</td>\n",
       "      <td>1.151147</td>\n",
       "      <td>-0.096695</td>\n",
       "      <td>0.223050</td>\n",
       "      <td>-0.068384</td>\n",
       "      <td>0.577829</td>\n",
       "      <td>...</td>\n",
       "      <td>-0.164350</td>\n",
       "      <td>-0.295135</td>\n",
       "      <td>-0.072173</td>\n",
       "      <td>-0.450261</td>\n",
       "      <td>0.313267</td>\n",
       "      <td>-0.289617</td>\n",
       "      <td>0.002988</td>\n",
       "      <td>-0.015309</td>\n",
       "      <td>42.53</td>\n",
       "      <td>1</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>5 rows × 31 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "            Time        V1        V2        V3        V4        V5        V6  \\\n",
       "279863  169142.0 -1.927883  1.125653 -4.518331  1.749293 -1.566487 -2.010494   \n",
       "280143  169347.0  1.378559  1.289381 -5.004247  1.411850  0.442581 -1.326536   \n",
       "280149  169351.0 -0.676143  1.126366 -2.213700  0.468308 -1.120541 -0.003346   \n",
       "281144  169966.0 -3.113832  0.585864 -5.399730  1.817092 -0.840618 -2.943548   \n",
       "281674  170348.0  1.991976  0.158476 -2.583441  0.408670  1.151147 -0.096695   \n",
       "\n",
       "              V7        V8        V9  ...       V21       V22       V23  \\\n",
       "279863 -0.882850  0.697211 -2.064945  ...  0.778584 -0.319189  0.639419   \n",
       "280143 -1.413170  0.248525 -1.127396  ...  0.370612  0.028234 -0.145640   \n",
       "280149 -2.234739  1.210158 -0.652250  ...  0.751826  0.834108  0.190944   \n",
       "281144 -2.208002  1.058733 -1.632333  ...  0.583276 -0.269209 -0.456108   \n",
       "281674  0.223050 -0.068384  0.577829  ... -0.164350 -0.295135 -0.072173   \n",
       "\n",
       "             V24       V25       V26       V27       V28  Amount  Class  \n",
       "279863 -0.294885  0.537503  0.788395  0.292680  0.147968  390.00      1  \n",
       "280143 -0.081049  0.521875  0.739467  0.389152  0.186637    0.76      1  \n",
       "280149  0.032070 -0.739695  0.471111  0.385107  0.194361   77.89      1  \n",
       "281144 -0.183659 -0.328168  0.606116  0.884876 -0.253700  245.00      1  \n",
       "281674 -0.450261  0.313267 -0.289617  0.002988 -0.015309   42.53      1  \n",
       "\n",
       "[5 rows x 31 columns]"
      ]
     },
     "execution_count": 19,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "new_dataset.tail()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "id": "3c52b20c",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Class\n",
       "0    492\n",
       "1    492\n",
       "Name: count, dtype: int64"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "new_dataset['Class'].value_counts()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "id": "c32e6fde",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Time</th>\n",
       "      <th>V1</th>\n",
       "      <th>V2</th>\n",
       "      <th>V3</th>\n",
       "      <th>V4</th>\n",
       "      <th>V5</th>\n",
       "      <th>V6</th>\n",
       "      <th>V7</th>\n",
       "      <th>V8</th>\n",
       "      <th>V9</th>\n",
       "      <th>...</th>\n",
       "      <th>V20</th>\n",
       "      <th>V21</th>\n",
       "      <th>V22</th>\n",
       "      <th>V23</th>\n",
       "      <th>V24</th>\n",
       "      <th>V25</th>\n",
       "      <th>V26</th>\n",
       "      <th>V27</th>\n",
       "      <th>V28</th>\n",
       "      <th>Amount</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Class</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>93217.274390</td>\n",
       "      <td>0.056618</td>\n",
       "      <td>-0.113306</td>\n",
       "      <td>-0.068841</td>\n",
       "      <td>0.070802</td>\n",
       "      <td>0.073465</td>\n",
       "      <td>-0.021720</td>\n",
       "      <td>-0.005135</td>\n",
       "      <td>0.072233</td>\n",
       "      <td>-0.030199</td>\n",
       "      <td>...</td>\n",
       "      <td>0.019525</td>\n",
       "      <td>-0.017278</td>\n",
       "      <td>0.000232</td>\n",
       "      <td>-0.024796</td>\n",
       "      <td>0.01904</td>\n",
       "      <td>-0.064227</td>\n",
       "      <td>0.022372</td>\n",
       "      <td>0.025798</td>\n",
       "      <td>-0.017661</td>\n",
       "      <td>99.251463</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>80746.806911</td>\n",
       "      <td>-4.771948</td>\n",
       "      <td>3.623778</td>\n",
       "      <td>-7.033281</td>\n",
       "      <td>4.542029</td>\n",
       "      <td>-3.151225</td>\n",
       "      <td>-1.397737</td>\n",
       "      <td>-5.568731</td>\n",
       "      <td>0.570636</td>\n",
       "      <td>-2.581123</td>\n",
       "      <td>...</td>\n",
       "      <td>0.372319</td>\n",
       "      <td>0.713588</td>\n",
       "      <td>0.014049</td>\n",
       "      <td>-0.040308</td>\n",
       "      <td>-0.10513</td>\n",
       "      <td>0.041449</td>\n",
       "      <td>0.051648</td>\n",
       "      <td>0.170575</td>\n",
       "      <td>0.075667</td>\n",
       "      <td>122.211321</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "<p>2 rows × 30 columns</p>\n",
       "</div>"
      ],
      "text/plain": [
       "               Time        V1        V2        V3        V4        V5  \\\n",
       "Class                                                                   \n",
       "0      93217.274390  0.056618 -0.113306 -0.068841  0.070802  0.073465   \n",
       "1      80746.806911 -4.771948  3.623778 -7.033281  4.542029 -3.151225   \n",
       "\n",
       "             V6        V7        V8        V9  ...       V20       V21  \\\n",
       "Class                                          ...                       \n",
       "0     -0.021720 -0.005135  0.072233 -0.030199  ...  0.019525 -0.017278   \n",
       "1     -1.397737 -5.568731  0.570636 -2.581123  ...  0.372319  0.713588   \n",
       "\n",
       "            V22       V23      V24       V25       V26       V27       V28  \\\n",
       "Class                                                                        \n",
       "0      0.000232 -0.024796  0.01904 -0.064227  0.022372  0.025798 -0.017661   \n",
       "1      0.014049 -0.040308 -0.10513  0.041449  0.051648  0.170575  0.075667   \n",
       "\n",
       "           Amount  \n",
       "Class              \n",
       "0       99.251463  \n",
       "1      122.211321  \n",
       "\n",
       "[2 rows x 30 columns]"
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "new_dataset.groupby('Class').mean()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 22,
   "id": "af7c21f3",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Splitting the data\n",
    "X = new_dataset.drop(columns='Class', axis=1)\n",
    "Y = new_dataset['Class']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 23,
   "id": "6dbffa8b",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "            Time        V1        V2        V3        V4         V5        V6  \\\n",
      "177198  123080.0  1.973186 -0.641150 -0.542609  0.341897  -0.577897  0.050004   \n",
      "151075   94537.0  1.719386  0.402091 -0.899124  3.611173   1.257730  1.579898   \n",
      "177683  123290.0 -5.439683 -4.147777 -5.959422 -0.887167 -13.689013  7.845434   \n",
      "85531    60808.0 -3.940556 -3.915472  1.895930  0.716928   3.982146 -3.180268   \n",
      "188135  127833.0 -1.606631 -0.832683  0.255481 -0.601391   2.788026 -1.748567   \n",
      "...          ...       ...       ...       ...       ...        ...       ...   \n",
      "279863  169142.0 -1.927883  1.125653 -4.518331  1.749293  -1.566487 -2.010494   \n",
      "280143  169347.0  1.378559  1.289381 -5.004247  1.411850   0.442581 -1.326536   \n",
      "280149  169351.0 -0.676143  1.126366 -2.213700  0.468308  -1.120541 -0.003346   \n",
      "281144  169966.0 -3.113832  0.585864 -5.399730  1.817092  -0.840618 -2.943548   \n",
      "281674  170348.0  1.991976  0.158476 -2.583441  0.408670   1.151147 -0.096695   \n",
      "\n",
      "               V7        V8        V9  ...       V20       V21       V22  \\\n",
      "177198  -0.806373  0.161339  1.496749  ... -0.214710  0.135113  0.468296   \n",
      "151075  -0.086648  0.311985 -0.045239  ... -0.359593  0.215670  0.854776   \n",
      "177683  12.571331 -1.169319 -1.840041  ... -2.105628 -0.997839 -0.028644   \n",
      "85531   -1.881820 -0.178257  0.954933  ... -0.503639 -0.396018 -0.429042   \n",
      "188135  -0.122949  0.152840 -0.428752  ...  0.311140 -0.066507 -0.782261   \n",
      "...           ...       ...       ...  ...       ...       ...       ...   \n",
      "279863  -0.882850  0.697211 -2.064945  ...  1.252967  0.778584 -0.319189   \n",
      "280143  -1.413170  0.248525 -1.127396  ...  0.226138  0.370612  0.028234   \n",
      "280149  -2.234739  1.210158 -0.652250  ...  0.247968  0.751826  0.834108   \n",
      "281144  -2.208002  1.058733 -1.632333  ...  0.306271  0.583276 -0.269209   \n",
      "281674   0.223050 -0.068384  0.577829  ... -0.017652 -0.164350 -0.295135   \n",
      "\n",
      "             V23       V24       V25       V26       V27       V28   Amount  \n",
      "177198  0.169180  0.431069 -0.292862  0.560037 -0.034632 -0.043273    28.75  \n",
      "151075  0.084477 -1.450250 -0.143424  0.188958 -0.033348 -0.077165    43.24  \n",
      "177683  1.875669  0.590515 -0.456819 -0.687225  2.529994 -2.177994  3017.28  \n",
      "85531  -0.578267  0.637504 -0.348859  0.012972  0.379042 -0.380173    78.41  \n",
      "188135  0.300438  0.651297 -0.375981  0.001595  0.009563  0.207905     1.98  \n",
      "...          ...       ...       ...       ...       ...       ...      ...  \n",
      "279863  0.639419 -0.294885  0.537503  0.788395  0.292680  0.147968   390.00  \n",
      "280143 -0.145640 -0.081049  0.521875  0.739467  0.389152  0.186637     0.76  \n",
      "280149  0.190944  0.032070 -0.739695  0.471111  0.385107  0.194361    77.89  \n",
      "281144 -0.456108 -0.183659 -0.328168  0.606116  0.884876 -0.253700   245.00  \n",
      "281674 -0.072173 -0.450261  0.313267 -0.289617  0.002988 -0.015309    42.53  \n",
      "\n",
      "[984 rows x 30 columns]\n"
     ]
    }
   ],
   "source": [
    "print(X)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 24,
   "id": "084b9f74",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "177198    0\n",
      "151075    0\n",
      "177683    0\n",
      "85531     0\n",
      "188135    0\n",
      "         ..\n",
      "279863    1\n",
      "280143    1\n",
      "280149    1\n",
      "281144    1\n",
      "281674    1\n",
      "Name: Class, Length: 984, dtype: int64\n"
     ]
    }
   ],
   "source": [
    "print(Y)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "5b07a88a",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Split the data into train and test data\n",
    "X_train, X_test, Y_train, Y_test =train_test_split(X, Y, test_size=0.2, stratify=Y, random_state=42)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "fd7bdad4",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "(984, 30) (787, 30) (197, 30)\n"
     ]
    }
   ],
   "source": [
    "print(X.shape, X_train.shape, X_test.shape)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "6bdf2e20",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Model training \n",
    "\n",
    "# Logistic Regression\n",
    "model = LogisticRegression()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 28,
   "id": "2f243530",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Dell\\anaconda3\\Lib\\site-packages\\sklearn\\linear_model\\_logistic.py:460: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "Please also refer to the documentation for alternative solver options:\n",
      "    https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression\n",
      "  n_iter_i = _check_optimize_result(\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-1 {color: black;}#sk-container-id-1 pre{padding: 0;}#sk-container-id-1 div.sk-toggleable {background-color: white;}#sk-container-id-1 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-1 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-1 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-1 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-1 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-1 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-1 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-1 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-1 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-1 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-1 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-1 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-1 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-1 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-1 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-1 div.sk-item {position: relative;z-index: 1;}#sk-container-id-1 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-1 div.sk-item::before, #sk-container-id-1 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-1 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-1 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-1 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-1 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-1 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-1 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-1 div.sk-label-container {text-align: center;}#sk-container-id-1 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-1 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-1\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>LogisticRegression()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-1\" type=\"checkbox\" checked><label for=\"sk-estimator-id-1\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">LogisticRegression</label><div class=\"sk-toggleable__content\"><pre>LogisticRegression()</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "LogisticRegression()"
      ]
     },
     "execution_count": 28,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Trainning logistic model with trainning dataset\n",
    "model.fit(X_train, Y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 29,
   "id": "05d38fa6",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Model Evaluation\n",
    "#accuracy on training data\n",
    "X_train_prediction =   model.predict(X_train)\n",
    "training_data_accuracy = accuracy_score(X_train_prediction, Y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 30,
   "id": "7d91e4e9",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Accuracy on ta=raining data : 0.9377382465057179\n"
     ]
    }
   ],
   "source": [
    "print('Accuracy on ta=raining data :', training_data_accuracy)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 31,
   "id": "cea672ab",
   "metadata": {},
   "outputs": [],
   "source": [
    "#accuracy on test data\n",
    "X_test_prediction =   model.predict(X_test)\n",
    "testing_data_accuracy = accuracy_score(X_test_prediction, Y_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 32,
   "id": "0ffa0b16",
   "metadata": {},
   "outputs": [
    {
     "name": "stderr",
     "output_type": "stream",
     "text": [
      "C:\\Users\\Dell\\anaconda3\\Lib\\site-packages\\sklearn\\linear_model\\_logistic.py:460: ConvergenceWarning: lbfgs failed to converge (status=1):\n",
      "STOP: TOTAL NO. of ITERATIONS REACHED LIMIT.\n",
      "\n",
      "Increase the number of iterations (max_iter) or scale the data as shown in:\n",
      "    https://scikit-learn.org/stable/modules/preprocessing.html\n",
      "Please also refer to the documentation for alternative solver options:\n",
      "    https://scikit-learn.org/stable/modules/linear_model.html#logistic-regression\n",
      "  n_iter_i = _check_optimize_result(\n"
     ]
    },
    {
     "data": {
      "text/html": [
       "<style>#sk-container-id-2 {color: black;}#sk-container-id-2 pre{padding: 0;}#sk-container-id-2 div.sk-toggleable {background-color: white;}#sk-container-id-2 label.sk-toggleable__label {cursor: pointer;display: block;width: 100%;margin-bottom: 0;padding: 0.3em;box-sizing: border-box;text-align: center;}#sk-container-id-2 label.sk-toggleable__label-arrow:before {content: \"▸\";float: left;margin-right: 0.25em;color: #696969;}#sk-container-id-2 label.sk-toggleable__label-arrow:hover:before {color: black;}#sk-container-id-2 div.sk-estimator:hover label.sk-toggleable__label-arrow:before {color: black;}#sk-container-id-2 div.sk-toggleable__content {max-height: 0;max-width: 0;overflow: hidden;text-align: left;background-color: #f0f8ff;}#sk-container-id-2 div.sk-toggleable__content pre {margin: 0.2em;color: black;border-radius: 0.25em;background-color: #f0f8ff;}#sk-container-id-2 input.sk-toggleable__control:checked~div.sk-toggleable__content {max-height: 200px;max-width: 100%;overflow: auto;}#sk-container-id-2 input.sk-toggleable__control:checked~label.sk-toggleable__label-arrow:before {content: \"▾\";}#sk-container-id-2 div.sk-estimator input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-label input.sk-toggleable__control:checked~label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 input.sk-hidden--visually {border: 0;clip: rect(1px 1px 1px 1px);clip: rect(1px, 1px, 1px, 1px);height: 1px;margin: -1px;overflow: hidden;padding: 0;position: absolute;width: 1px;}#sk-container-id-2 div.sk-estimator {font-family: monospace;background-color: #f0f8ff;border: 1px dotted black;border-radius: 0.25em;box-sizing: border-box;margin-bottom: 0.5em;}#sk-container-id-2 div.sk-estimator:hover {background-color: #d4ebff;}#sk-container-id-2 div.sk-parallel-item::after {content: \"\";width: 100%;border-bottom: 1px solid gray;flex-grow: 1;}#sk-container-id-2 div.sk-label:hover label.sk-toggleable__label {background-color: #d4ebff;}#sk-container-id-2 div.sk-serial::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: 0;}#sk-container-id-2 div.sk-serial {display: flex;flex-direction: column;align-items: center;background-color: white;padding-right: 0.2em;padding-left: 0.2em;position: relative;}#sk-container-id-2 div.sk-item {position: relative;z-index: 1;}#sk-container-id-2 div.sk-parallel {display: flex;align-items: stretch;justify-content: center;background-color: white;position: relative;}#sk-container-id-2 div.sk-item::before, #sk-container-id-2 div.sk-parallel-item::before {content: \"\";position: absolute;border-left: 1px solid gray;box-sizing: border-box;top: 0;bottom: 0;left: 50%;z-index: -1;}#sk-container-id-2 div.sk-parallel-item {display: flex;flex-direction: column;z-index: 1;position: relative;background-color: white;}#sk-container-id-2 div.sk-parallel-item:first-child::after {align-self: flex-end;width: 50%;}#sk-container-id-2 div.sk-parallel-item:last-child::after {align-self: flex-start;width: 50%;}#sk-container-id-2 div.sk-parallel-item:only-child::after {width: 0;}#sk-container-id-2 div.sk-dashed-wrapped {border: 1px dashed gray;margin: 0 0.4em 0.5em 0.4em;box-sizing: border-box;padding-bottom: 0.4em;background-color: white;}#sk-container-id-2 div.sk-label label {font-family: monospace;font-weight: bold;display: inline-block;line-height: 1.2em;}#sk-container-id-2 div.sk-label-container {text-align: center;}#sk-container-id-2 div.sk-container {/* jupyter's `normalize.less` sets `[hidden] { display: none; }` but bootstrap.min.css set `[hidden] { display: none !important; }` so we also need the `!important` here to be able to override the default hidden behavior on the sphinx rendered scikit-learn.org. See: https://github.com/scikit-learn/scikit-learn/issues/21755 */display: inline-block !important;position: relative;}#sk-container-id-2 div.sk-text-repr-fallback {display: none;}</style><div id=\"sk-container-id-2\" class=\"sk-top-container\"><div class=\"sk-text-repr-fallback\"><pre>LogisticRegression()</pre><b>In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook. <br />On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.</b></div><div class=\"sk-container\" hidden><div class=\"sk-item\"><div class=\"sk-estimator sk-toggleable\"><input class=\"sk-toggleable__control sk-hidden--visually\" id=\"sk-estimator-id-2\" type=\"checkbox\" checked><label for=\"sk-estimator-id-2\" class=\"sk-toggleable__label sk-toggleable__label-arrow\">LogisticRegression</label><div class=\"sk-toggleable__content\"><pre>LogisticRegression()</pre></div></div></div></div></div>"
      ],
      "text/plain": [
       "LogisticRegression()"
      ]
     },
     "execution_count": 32,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "log = LogisticRegression()\n",
    "log.fit(X_train,Y_train)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 33,
   "id": "c12870d3",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9494949494949495"
      ]
     },
     "execution_count": 33,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y_pred1 = log.predict(X_test)\n",
    "precision_score(Y_test,Y_pred1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 34,
   "id": "aa142277",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9494949494949495"
      ]
     },
     "execution_count": 34,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "precision_score(Y_test,Y_pred1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 35,
   "id": "f9fa5651",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9591836734693877"
      ]
     },
     "execution_count": 35,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "recall_score(Y_test,Y_pred1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 36,
   "id": "0763db77",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9591836734693877"
      ]
     },
     "execution_count": 36,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "recall_score(Y_test,Y_pred1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 37,
   "id": "30cac590",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9543147208121828"
      ]
     },
     "execution_count": 37,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "f1_score(Y_test,Y_pred1)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 38,
   "id": "cef460d9",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Decision tree classifier\n",
    "dt = DecisionTreeClassifier()\n",
    "dt.fit(X_train,Y_train)\n",
    "DecisionTreeClassifier()\n",
    "Y_pred2 = dt.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 39,
   "id": "96bb9280",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8781725888324873"
      ]
     },
     "execution_count": 39,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "accuracy_score(Y_test,Y_pred2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 40,
   "id": "84ced4d6",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8363636363636363"
      ]
     },
     "execution_count": 40,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "precision_score(Y_test,Y_pred2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "7b0849fd",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8846153846153846"
      ]
     },
     "execution_count": 41,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "f1_score(Y_test,Y_pred2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "c434f7af",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9387755102040817"
      ]
     },
     "execution_count": 42,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "recall_score(Y_test,Y_pred2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "57e100f6",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.8846153846153846"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "f1_score(Y_test,Y_pred2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 44,
   "id": "d89ad2d5",
   "metadata": {},
   "outputs": [],
   "source": [
    "#Random forest classifier\n",
    "rf = RandomForestClassifier()\n",
    "rf.fit(X_train,Y_train)\n",
    "Y_pred3 = rf.predict(X_test)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 45,
   "id": "6e9b9386",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.949238578680203"
      ]
     },
     "execution_count": 45,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "accuracy_score(Y_test,Y_pred3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 46,
   "id": "1ff01ebd",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9489795918367347"
      ]
     },
     "execution_count": 46,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "precision_score(Y_test,Y_pred3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 47,
   "id": "f00d7fd8",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9489795918367347"
      ]
     },
     "execution_count": 47,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "recall_score(Y_test,Y_pred3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 48,
   "id": "c6958329",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "0.9489795918367347"
      ]
     },
     "execution_count": 48,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "f1_score(Y_test,Y_pred3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 49,
   "id": "18f43ddb",
   "metadata": {},
   "outputs": [],
   "source": [
    "#final data with comparison\n",
    "final_data = pd.DataFrame({'Models':['LR','DT','RF'],\n",
    "              \"ACC\":[accuracy_score(Y_test,Y_pred1)*100,\n",
    "                     accuracy_score(Y_test,Y_pred2)*100,\n",
    "                     accuracy_score(Y_test,Y_pred3)*100\n",
    "                    ]})"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 50,
   "id": "84ead114",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "  Models        ACC\n",
      "0     LR  95.431472\n",
      "1     DT  87.817259\n",
      "2     RF  94.923858\n"
     ]
    }
   ],
   "source": [
    "print(final_data)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "id": "9285c00b",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<Axes: xlabel='Models', ylabel='ACC'>"
      ]
     },
     "execution_count": 54,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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smXLmnZQAABgS7be2SkqKtIjjzyiN998U23btr3oOofD4XPbsqwG586XmJiosrIy71FUVNRkMwMAAHux9c5OXl6eSkpKNGTIEO+52tpaffTRR0pPT9eRI0ck/bjD061bN++akpKSBrs953M6nXI6nc03OAAAsA1b7+zceuutOnTokA4cOOA9hg4dqvvvv18HDhzQNddcI7fbraysLO99ampqlJ2drejoaD9ODgAA7MLWOzshISHq37+/z7l27dqpc+fO3vPx8fFKSkpSVFSUoqKilJSUpODgYE2bNs0fIwMAAJuxdew0RkJCgqqqqhQXF6fS0lINHz5cmZmZCgkJ8fdoAADABlpc7OzevdvntsPhkMfjkcfj8cs8AADA3mz9mR0AAIBLRewAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaMQOAAAwGrEDAACMRuwAAACjETsAAMBoto6d5ORkDRs2TCEhIerataumTJmiI0eO+KyxLEsej0fh4eEKCgrSmDFjlJ+f76eJAQCA3dg6drKzszV//nx98sknysrK0rlz5xQTE6MzZ85416SkpCg1NVXp6enKzc2V2+3WuHHjVFFR4cfJAQCAXbT29wA/ZceOHT63169fr65duyovL08333yzLMtSWlqali5dqqlTp0qSMjIy5HK5tHHjRsXGxvpjbAAAYCO23tn5X2VlZZKkTp06SZIKCwtVXFysmJgY7xqn06nRo0crJyfnoo9TXV2t8vJynwMAAJipxcSOZVlavHixbrzxRvXv31+SVFxcLEly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3r17a8CAAVq1apWqq6u1bNkynzX13zPrjw4dOvhnWIMRO2hWHTt21MKFC/X444/z4+e47Hbt2qVDhw7p7rvv9vcogCTp2Wef1YsvvqgTJ074e5QrCrGDX6WsrEwHDhzwOY4fP37BtfPnz9eRI0e0ZcuWyzwlriTV1dUqLi7WN998o/379yspKUmTJ0/WpEmT9OCDD/p7PECSNGbMGF1//fVKSkry9yhXFD6zg19l9+7dGjRokM+5GTNmXHDtVVddpenTp8vj8Wjq1Klq1YrGRtPbsWOHunXrptatW6tjx44aOHCgVq1apRkzZvCag60sXrxYDz30UIMPKqP5OCzeWwAAAAbj/+4AAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsALgi7N69Ww6HQ99//32j79OrVy+lpaU120wALg9iB4AtzJw5Uw6HQ3Pnzm1wLS4uTg6HQzNnzrz8gwFo8YgdALYRERGhzZs3q6qqynvuhx9+0KZNm9SjRw8/TgagJSN2ANjG4MGD1aNHD23dutV7buvWrYqIiPD5w7PV1dVatGiRunbtqrZt2+rGG29Ubm6uz2Nt375d1157rYKCgjR27Fh99dVXDb5eTk6Obr75ZgUFBSkiIkKLFi3SmTNnLjqfx+NRjx495HQ6FR4erkWLFl36kwbQ7IgdALby0EMPaf369d7br732mmbNmuWzJiEhQVu2bFFGRob279+v3r17a/z48fruu+8kSUVFRZo6daomTJigAwcOaPbs2XryySd9HuPQoUMaP368pk6dqoMHD+qtt97S3r17tWDBggvO9fbbb2vlypX685//rC+++ELvvPOObrjhhiZ+9gCahQUANjBjxgxr8uTJ1qlTpyyn02kVFhZaX331ldW2bVvr1KlT1uTJk60ZM2ZYp0+ftgIDA62//e1v3vvW1NRY4eHhVkpKimVZlpWYmGj17dvXqqur865ZsmSJJckqLS21LMuypk+fbv3pT3/ymWHPnj1Wq1atrKqqKsuyLKtnz57WypUrLcuyrJdeesm69tprrZqammb8VwDQHNjZAWArXbp00cSJE5WRkaH169dr4sSJ6tKli/f6v//9b509e1ajRo3yngsMDNTvfvc7FRQUSJIKCgo0YsQIORwO75qRI0f6fJ28vDxt2LBB7du39x7jx49XXV2dCgsLG8x1zz33qKqqStdcc43mzJmjbdu26dy5c0399AE0g9b+HgAA/tesWbO8bye9/PLLPtcsy5Ikn5CpP19/rn7NT6mrq1NsbOwFP3dzoQ9DR0RE6MiRI8rKytLOnTsVFxenF154QdnZ2QoMDGzcEwPgF+zsALCd22+/XTU1NaqpqdH48eN9rvXu3Vtt2rTR3r17vefOnj2rffv2qW/fvpKkfv366ZNPPvG53//eHjx4sPLz89W7d+8GR5s2bS44V1BQkO666y6tWrVKu3fv1scff6xDhw41xVMG0IzY2QFgOwEBAd63pAICAnyutWvXTvPmzdMTTzyhTp06qUePHkpJSVFlZaUefvhhSdLcuXP10ksvafHixYqNjfW+ZXW+JUuWaMSIEZo/f77mzJmjdu3aqaCgQFlZWVq9enWDmTZs2KDa2loNHz5cwcHBeuONNxQUFKSePXs2zz8CgCbDzg4AWwoNDVVoaOgFrz333HO6++67NX36dA0ePFhHjx7VBx98oI4dO0r68W2oLVu26L333tPAgQP16quvKikpyecxBgwYoOzsbH3xxRe66aabNGjQID399NPq1q3bBb9mhw4dtG7dOo0aNUoDBgzQhx9+qPfee0+dO3du2icOoMk5rMa8uQ0AANBCsbMDAACMRuwAAACjETsAAMBoxA4AADAasQMAAIxG7AAAAKMROwAAwGjEDgAAMBqxAwAAjEbsAAAAoxE7AADAaP8P1dqxH5dekpUAAAAASUVORK5CYII=",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "sns.barplot(x = 'Models', y = 'ACC', data= final_data)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "id": "2f612ebd",
   "metadata": {},
   "outputs": [],
   "source": [
    "X = credit_card_data.drop('Class',axis=1)\n",
    "Y = credit_card_data['Class']"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 56,
   "id": "ded76274",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(284807, 30)"
      ]
     },
     "execution_count": 56,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "X.shape"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 57,
   "id": "7f017931",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "(284807,)"
      ]
     },
     "execution_count": 57,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Y.shape"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
