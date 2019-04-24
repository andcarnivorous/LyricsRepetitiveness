
# Table of Contents

1.  [Loading percentages](#org4b50479)
2.  [Distributions](#orgec5bc04)
3.  [Shapiro Test](#org629773e)
4.  [Welch T-Tests](#org8676a12)
5.  [Mann Whitney U Test](#orgff292ec)
6.  [Anova](#org0b57525)


<a id="org4b50479"></a>

# Loading percentages

    
    import pickle
    
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)


<a id="orgec5bc04"></a>

# Distributions

    
    import pickle
    import seaborn as sns
    import matplotlib.pyplot as plt
    
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)
    
    
    data = {"Italian" : italianpercs, 
    	"English" : englishpercs,
    	"Dutch" : dutchpercs,
    	"modernDutch" : moderndutchpercs,
    	"oldEnglish" : oldenglishpercs}
    
    for x in data.items():
      sns.distplot(x[1], label=x[0])
    plt.legend()
    plt.savefig("plotto.png")
    return "./plotto.png"

![img](./plotto.png)


<a id="org629773e"></a>

# Shapiro Test

    import pickle
    from scipy import stats
    import pylab
    import matplotlib.pyplot as plt
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)
    
    
    data = {"Italian" : italianpercs, 
    	"English" : englishpercs,
    	"Dutch" : dutchpercs,
    	"modernDutch" : moderndutchpercs,
    	"OldEng" : oldenglishpercs}
    
    results = dict()
    
    for x in data.items():
      stats.probplot(x[1], dist="norm", plot=pylab)
      plt.title(x[0])
      plt.savefig("%sQQplot.png" % x[0])
      plt.close("all")
      results[x[0]] = stats.shapiro(x[1])[1]
    
    
    return results

<table border="2" cellspacing="0" cellpadding="6" rules="groups" frame="hsides">


<colgroup>
<col  class="org-left" />

<col  class="org-left" />

<col  class="org-right" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-right" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-right" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-right" />

<col  class="org-left" />

<col  class="org-left" />

<col  class="org-right" />
</colgroup>
<tbody>
<tr>
<td class="org-left">Italian</td>
<td class="org-left">:</td>
<td class="org-right">0.420023113489151</td>
<td class="org-left">English</td>
<td class="org-left">:</td>
<td class="org-right">3.952866822370328e-23</td>
<td class="org-left">Dutch</td>
<td class="org-left">:</td>
<td class="org-right">3.278021409869325e-08</td>
<td class="org-left">modernDutch</td>
<td class="org-left">:</td>
<td class="org-right">2.2561225705430843e-05</td>
<td class="org-left">OldEng</td>
<td class="org-left">:</td>
<td class="org-right">2.797007780941385e-08</td>
</tr>
</tbody>
</table>


<a id="org8676a12"></a>

# Welch T-Tests

    
    import pickle
    
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)
    
    import seaborn as sns
    from scipy import stats
    import pylab
    
    dutcheng = "DUTCH ENG:\t"+str(stats.ttest_ind(dutchpercs, englishpercs)[1])
    dutchita = "DUTCH ITA:\t"+str(stats.ttest_ind(dutchpercs, italianpercs)[1])
    dutchmod = "DUTCH MODDutch:\t"+str(stats.ttest_ind(dutchpercs, moderndutchpercs)[1])
    italeng = "ITA ENG:\t"+str(stats.ttest_ind(italianpercs, englishpercs)[1])
    italmod = "ITA MODDutch:\t"+str(stats.ttest_ind(italianpercs, moderndutchpercs)[1])
    engmod = "ENG MODDutch:\t"+str(stats.ttest_ind(englishpercs, moderndutchpercs)[1])
    oldengdutch = "OLDENG DUTCH:\t"+str(stats.ttest_ind(oldenglishpercs, dutchpercs)[1])
    oldengmod = "OLDENG MODDutch:"+str(stats.ttest_ind(oldenglishpercs, moderndutchpercs)[1])
    oldengital = "OLDENG ITA:\t"+str(stats.ttest_ind(oldenglishpercs, italianpercs)[1])
    oldengeng = "OLDENG ENG:\t"+str(stats.ttest_ind(oldenglishpercs, englishpercs)[1])
    
    return "\n".join([dutcheng, dutchita,dutchmod, italeng, italmod, engmod, oldengdutch, oldengmod, oldengital,oldengeng])

    DUTCH ENG:	1.4356427109517667e-81
    DUTCH ITA:	2.9341870715988103e-18
    DUTCH MODDutch:	1.1591052795152356e-09
    ITA ENG:	5.076797349634289e-52
    ITA MODDutch:	0.07694328188116538
    ENG MODDutch:	6.561047780002253e-58
    OLDENG DUTCH:	3.4796258286786167e-59
    OLDENG MODDutch:7.4986282747156e-90
    OLDENG ITA:	4.490154633877362e-125
    OLDENG ENG:	0.0


<a id="orgff292ec"></a>

# Mann Whitney U Test

    
    import pickle
    
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)
    
    
    import seaborn as sns
    from scipy import stats
    import pylab
    
    dutcheng = "DUTCH ENG:\t"+str(stats.mannwhitneyu(dutchpercs, englishpercs)[1])
    dutchita = "DUTCH ITA:\t"+str(stats.mannwhitneyu(dutchpercs, italianpercs)[1])
    dutchmod = "DUTCH MODDutch:\t"+str(stats.mannwhitneyu(dutchpercs, moderndutchpercs)[1])
    italeng = "ITA ENG:\t"+str(stats.mannwhitneyu(italianpercs, englishpercs)[1])
    italmod = "ITA MODDutch:\t"+str(stats.mannwhitneyu(italianpercs, moderndutchpercs)[1])
    engmod = "ENG MODDutch:\t"+str(stats.mannwhitneyu(englishpercs, moderndutchpercs)[1])
    oldengdutch = "OLDENG DUTCH:\t"+str(stats.mannwhitneyu(oldenglishpercs, dutchpercs)[1])
    oldengmod = "OLDENG MODDutch:"+str(stats.mannwhitneyu(oldenglishpercs, moderndutchpercs)[1])
    oldengital = "OLDENG ITA:\t"+str(stats.mannwhitneyu(oldenglishpercs, italianpercs)[1])
    oldengeng = "OLDENG ENG:\t"+str(stats.mannwhitneyu(oldenglishpercs, englishpercs)[1])
    
    return "\n".join([dutcheng, dutchita,dutchmod, italeng, italmod, engmod, oldengdutch, oldengmod, oldengital,oldengeng])

    DUTCH ENG:	1.3717168636704838e-79
    DUTCH ITA:	5.88518398092256e-21
    DUTCH MODDutch:	6.18417694118659e-11
    ITA ENG:	1.4977812914162474e-49
    ITA MODDutch:	0.01887171365553699
    ENG MODDutch:	2.916518520191118e-50
    OLDENG DUTCH:	3.794422495362001e-61
    OLDENG MODDutch:9.054563863042377e-82
    OLDENG ITA:	4.507989481863868e-99
    OLDENG ENG:	7.86121871245955e-176


<a id="org0b57525"></a>

# Anova

    
    import pickle
    
    italianpercs = open("italianpercs.pickle", "rb")
    italianpercs = pickle.load(italianpercs)
    
    englishpercs = open("englishpercs.pickle", "rb")
    englishpercs = pickle.load(englishpercs)
    
    dutchpercs = open("dutchpercs.pickle", "rb")
    dutchpercs = pickle.load(dutchpercs)
    
    moderndutchpercs = open("moderndutch.pickle", "rb")
    moderndutchpercs = pickle.load(moderndutchpercs)
    
    oldenglishpercs = open("oldenglishpercs.pickle", "rb")
    oldenglishpercs = pickle.load(oldenglishpercs)
    
    import seaborn as sns
    from scipy import stats
    import pylab
    
    return stats.f_oneway(dutchpercs, italianpercs, moderndutchpercs, englishpercs, oldenglishpercs)

    F_onewayResult(statistic=750.1551965115311, pvalue=0.0)

