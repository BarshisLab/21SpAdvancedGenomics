## 27-April-2016 - Filter contigs over 500
  - Created a new folder calles "assembly" under "Red Sea" and copied the assembly file "Trinity.fasta" from the filtered sequences 
  - Renamed the assembly file --> "Filtered_Trinity.fasta"

```
[ysawall@turing1 assembly]$ pwd
/cm/shared/courses/dbarshis/RedSea/assembly
[ysawall@turing1 assembly]$ ls
Filtered_Trinity.fasta
```
  - Run script (in the scripts folder of Dan)
  
```
[ysawall@turing1 assembly]$ ../../../dbarshis/15AdvBioinf/scripts/fasta_len_filter_dict_advbioinf.py 500 Filtered_Trinity.fasta
Number of total seqs for Filtered_Trinity.fasta: 557311
Number of seqs over 500 for Filtered_Trinity.fasta: 264159
[ysawall@turing1 assembly]$ ls
Filtered_Trinity.fasta  Filtered_Trinity_over500.fasta
```

(new fasta file created)
  * Started qrsh session
  * Created new folder for blast data bases (blastdb) under Red Sea and copied Dan's 4 databases into the new folder

```
[ysawall@turing1 assembly]$ qrsh
[ysawall@cr-053 ~]$ mkdir /cm/shared/courses/dbarshis/RedSea/blastdbs
[ysawall@cr-053 ~]$ cp /cm/shared/courses/dbarshis/15AdvBioinf/blastdbs/*.fasta /cm/shared/courses/dbarshis/RedSea/blastdbs
[ysawall@cr-053 ~]$ cd /cm/shared/courses/dbarshis/RedSea/blastdbs/
[ysawall@cr-053 blastdbs]$ ls
Allclean_coral_advbioinf.fasta  cleansym_advbioinf.fasta
Alldirtycoral_advbioinf.fasta   dirtysym_advbioinf.fasta
```
  * Module lead blast/2.2.29
  * Reformat databases into nucl format using the command "makeblastdb". Repeat for all 4 dbs.
```

[ysawall@cr-053 blastdbs]$ module load blast/2.2.29
[ysawall@cr-053 blastdbs]$ makeblastdb -in Allclean_coral_advbioinf.fasta -dbtype nucl -out cleancoral
[ysawall@cr-053 blastdbs]$ makeblastdb -in Alldirtycoral_advbioinf.fasta -dbtype nucl -out dirtycoral
[ysawall@cr-053 blastdbs]$ makeblastdb -in cleansym_advbioinf.fasta -dbtype nucl -out cleansym
[ysawall@cr-053 blastdbs]$ makeblastdb -in dirtysym_advbioinf.fasta -dbtype nucl -out dirtysym

[ysawall@cr-053 blastdbs]$ ls
Allclean_coral_advbioinf.fasta  cleansym.nhr    dirtysym_advbioinf.fasta
Alldirtycoral_advbioinf.fasta   cleansym.nin    dirtysym.nhr
cleancoral.nhr                  cleansym.nsq    dirtysym.nin
cleancoral.nin                  dirtycoral.nhr  dirtysym.nsq
cleancoral.nsq                  dirtycoral.nin
cleansym_advbioinf.fasta        dirtycoral.nsq
```


## 09-May-2016 - New blastdb for corals and symbionts (clean / dirty)

New sequences (fata files) for blastdb downloaded and placed in the new directory.
Files were downloaded (usually as .zip folders), then copied to the following directory using WinSCP, then unzipped, then all non-used files deleted (everything except the .fasta file)
```
[ysawall@turing1 New_sequences]$ pwd
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_sequences
[ysawall@turing1 New_sequences]$ unzip aten_july2014.zip
```

**Sequences of Sarah Davies list:**
(CC = clean coral, DC = dirty coral)
   - A. tenuis larvae (http://www.bio.utexas.edu/research/matz_lab/matzlab/Data.html) --> CC_AcropTunis_Matz2014.fasta
   - Aiptasia (gene model) (http://aiptasia.reefgenomics.org/download/) --> CC_Aiptasia_ReefGenomics.fasta
   - Acropora hyacinthus, Barshis et al. 2013 PNAS (http://palumbi.stanford.edu/data/) --> DC_AcropHya_Barshis2013.fasta
   - Acropora hyacinthus, Wright et al. 2015 (http://datadryad.org/resource/doi:10.5061/dryad.8mr56/8) **(NOT sure about the clean coral, because tissue from adult corals)**--> CC_AcropHya_Wright2015.fasta 
   - Anthopleura elegantissima, Kitchen et al. 2015 (http://datadryad.org/resource/doi:10.5061/dryad.3f08f/1) --> CC_AnthoEleg_Kitchen2015.fasta
   - Fungia scrutaria, Kitchen et al. 2015 (http://datadryad.org/resource/doi:10.5061/dryad.3f08f/2) --> DC_FungiaScru_Kitchen2015.fasta
   - Madracis auretenra, Meyer 2014 (http://people.oregonstate.edu/~meyere/data.html) --> DC_MadraAure_Kitchen2015.fasta
   - Montastraea cavernosa, Meyer 2014 (http://people.oregonstate.edu/~meyere/data.html) --> DC_MontaCaver_Meyer2014.fasta
   - Pseudodiploria strigosa, Meyer 2014 (http://people.oregonstate.edu/~meyere/data.html) **Clean coral??** --> CC_PseudodiplStri_Meyer2014.fasta
   - Seriatopora hystrix, Meyer 2014 (http://people.oregonstate.edu/~meyere/data.html) --> DC_SeriaHys_Meyer2014.fasta
   - Porites asteoides, Kenkel et al. 2013 (http://datadryad.org/resource/doi:10.5061/dryad.1kn38/1) --> DC_PorAst_Kenkel2013.fasta
   - Aiptasia pallida, Lehnert et al. 2012 (http://pringlelab.stanford.edu/projects.html - Adult aposymbiotic Aiptasia transcriptome version 1.1) --> CC_AiptPall_Lehnert2012.fasta

(CS = clean symbiont, DS = dirty symbiont)
   - Clade A (Kb8), cultured, Bayer et al. 2012 (http://medinalab.org/zoox/) --> CS_CladeA_Bayer2012.fasta
   - Clade B (Mf105), cultured, Bayer et al. 2012 (http://medinalab.org/zoox/) --> CS_CladeB_Bayer2012.fasta
   - Clade D1a (MMETSP1377) - Montastraea faveolata, Ruth Gates unpublished (http://data.imicrobe.us/sample/view/2219 - download-assembly) --> DS_CladeD1_Gates2011.fasta
   - Clade C - Acropora hyacinthus, Ladner et al. 2012 (http://palumbi.stanford.edu/data/) --> DS_CladeC_Ladner2012.fasta
   - Clade D - Acropora hyacinthus, Ladner et al. 2012 (http://palumbi.stanford.edu/data/) --> DS_CladeD_Ladner2012.fasta
   - Clade A - Tridacna crocea (MMETSP1374), Gates 2011, unpublished (http://data.imicrobe.us/sample/view/2193 - download-assembly) --> DS_CladeA_Gates2011.fasta
   - Clade C15 - Porites compressa (MMETSP1370), Gates 2011, unpublished (http://data.imicrobe.us/sample/view/2193 - download-assembly) --> DS_CladeC15a_Gates2011.fasta
   - Clade C15 - Porites compressa (MMETSP1371), Gates 2011, unpublished (http://data.imicrobe.us/sample/view/2193 - download-assembly) --> DS_CladeC15b_Gates2011.fasta
   - Clade C1 - Acropora tenuis (MMETSP1367), Gates 2011, unpublished (http://data.imicrobe.us/sample/view/2193 - download-assembly) --> DS_CladeC1a_Gates2011.fasta 
   - Clade C1 - Acropora tenuis (MMETSP1369), Gates 2011, unpublished (http://data.imicrobe.us/sample/view/2193 - download-assembly) --> DS_CladeC1b_Gates2011.fasta 


## 10-May-2016 - New blastdb for corals and symbionts (clean / dirty)
 
**Chris Voolstra list - additional sequences of corals**
   - Edwardsiella lineata, Stefanik et al. 2014, transcript produced 2009 (http://cnidarians.bu.edu/EdwardBase/cgi-bin/stock.cgi) --> DC_EdwardLinea_Stefanik2014.fasta
   - Favia sp., Pooyaei Mehr et al. 2013 (http://bmcgenomics.biomedcentral.com/articles/10.1186/1471-2164-14-546 - 2 FASTA files for cDNA region encoding for non-symbiont annotated ORFs in Fav1 and Fav2) --> CC_Favia1_Pooyaei2013.fasta; CC_Favia2_Pooyaei2013.fasta
   - Pocillopora damicornis, nubins of adult colonies, Traylor-Knowles et al. 2011, unpublished (http://cnidarians.bu.edu/PocilloporaBase/cgi-bin/pdamdata.cgi - Raw Reads used to assemble contigs) --> DC_PociDam_TraylorKnowles2011.fasta
   - Nematostella vectensis, Putnam et al. 2007, (ftp://ftp.jgi-psf.org/pub/JGI_data/Nematostella_vectensis/v1.0/assembly/Nemve1.fasta.gz) --> CC_NematVect_Putnam2007.fasta
   - clade-B1, cultured, Shoguchi et al. 2013 (http://marinegenomics.oist.jp/symb/viewer/info?project_id=21 - symbB1_v1.0.transcriptome_assembly.fa.gz) --> CS_CladeB1_Shonuchi2013.fasta
   - cultured Symbiodinium, 15 species, Zhange et al., 2007 (NCBI: AF512889, DQ864761–DQ864971, DQ867053–DQ867070, DQ884413–DQ884451, EF133854–EF133905, EF133961–EF134003, EF134083–EF134402, EF141835, and EF143070 –EF143105) --> CS_15SymbSP_Zhange2007.fasta
   - cultured freeliving Symbiodinium, Strain CCMP421, (MMETSP1110),  (http://mirrors.iplantcollaborative.org/browse/iplant/home/shared/imicrobe/projects/104/transcriptomes/MMETSP111/MMETSP1110.cds.fa) --> CS_StrainCCMP421_iMicrobe.fasta
   - cultured freeliving Symbiodinium, Strain CCMP2430, (MMETSP1115), " ,  --> CS_StrainCCMP2430a_iMicrobe.fasta
   - cultured freeliving Symbiodinium, Strain Mp,(MMETSP1122), " , --> CS_StrainMp1_iMicrobe.fasta
   - cultured freeliving Symbiodinium, Strain Mp,(MMETSP1123), " , --> CS_StrainMp2_iMicrobe.fasta
   - Acropora digitifera, sperm of colony, Shinzato et al. 2011 (NCBI: starting with NW_015441057..) --> CC_AcropDigi_Shinzato2011.fasta
   - Acropora palmata, eggs of colony, Schwarz et al. 2008 (NCBI: starting with DR982333...) --> CC_AcropPalm_Schwarz2008.fasta
   - Montastraea faveolata, eggs of colony, Schwarz et al. 2008 (NCBI: starting with R986350...) --> CC_MontaFaveo_Schwarz2008.fasta
   - Hydra vulgaris, Chapman et al. 2010, clean (NCBI: starting with NR_107860 ....) --> CC_HydraVul_Chapman2010.fasta 
   - Mnemiopsis leidyi, jellyfish, Ryan et al. 2013, Moreland et al. 2014 (http://research.nhgri.nih.gov/mnemiopsis/download/transcript/Ml_Cufflinks_transcripts.fa.gz) --> CC_MnemLei_Ryan2013.fasta
   - Monosiga brevicollis, cultured choanoflagellate, King et al. 2008 (JGI Genome portal, ftp://ftp.jgi-psf.org/pub/JGI_data/Monosiga_brevicollis/assembly/v1.0/Monbr1_scaffolds.fasta.gz) --> CS_MonoBrev_King2008.fasta
   - Pleurobranchia pileus, Ctenophore, Moroz et al. 2014, (http://neurobase.rc.ufl.edu/pleurobrachia/download - P-bachei_pileus_Illumina_RNA-seq) --> CC_PleuPil_Moroz2014.fasta
   - Platygyra carnosus, Sun et al. 2013 (wget http://www.comp.hkbu.edu.hk/~db/PcarnBase/db/nucleotide/CoralDNA CoralDNA.fasta [note the space, basically this saves the output of the CoralDNA webpage into a file called CoralDNA.fasta]) --> DC_PlatCarn_Sun2013.fasta
   - Gorgonia ventalina, Burge et al. 2013 (https://figshare.com/articles/Gorgonia_ventalina_transcriptome_/94326) --> DC_GorgVent_Burge2013.fasta 

To get sequences or files directly from the webpage use the command wget, e.g. (here the file is directly writen into a CoralDNA.fasta file)
```
[ysawall@turing1 New_sequences]$ wget http://www.comp.hkbu.edu.hk/~db/PcarnBase/db/nucleotide/CoralDNA CoralDNA.fasta
```

Summary of databases

```
[ysawall@turing1 New_sequences]$ pwd
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_sequences
[ysawall@turing1 New_sequences]$ ls
CC_AcropDigi_Shinzato2011.fasta    CS_StrainCCMP421_iMicrobe.fasta
CC_AcropHya_Wright2015.fasta       CS_StrainMp1_iMicrobe.fasta
CC_AcropPalm_Schwarz2008.fasta     CS_StrainMp2_iMicrobe.fasta
CC_AcropTunis_Matz2014.fasta       DC_AcropHya_Barshis2013.fasta
CC_Aiptasia_ReefGenomics.fasta     DC_EdwardLinea_Stefanik2014.fasta
CC_AiptPall_Lehnert2012.fasta      DC_FungiaScru_Kitchen2015.fasta
CC_AnthoEleg_Kitchen2015.fasta     DC_GorgVent_Burge2013.fasta
CC_Favia1_Pooyaei2013.fasta        DC_MadraAure_Kitchen2015.fasta
CC_Favia2_Pooyaei2013.fasta        DC_MontaCaver_Meyer2014.fasta
CC_HydraVul_Chapman2010.fasta      DC_PlatCarn_Sun2013.fasta
CC_MnemLei_Ryan2013.fasta          DC_PociDam_TraylorKnowles2011.fasta
CC_MontaFaveo_Schwarz2008.fasta    DC_PorAst_Kenkel2013.fasta
CC_NematVect_Putnam2007.fasta      DC_SeriaHys_Meyer2014.fasta
CC_PleuPil_Moroz2014.fasta         DS_CladeA_Gates2011.fasta
CC_PseudodiplStri_Meyer2014.fasta  DS_CladeC15a_Gates2011.fasta
CS_15SymbSP_Zhange2007.fasta       DS_CladeC15b_Gates2011.fasta
CS_CladeA_Bayer2012.fasta          DS_CladeC1a_Gates2011.fasta
CS_CladeB1_Shonuchi2013.fasta      DS_CladeC1b_Gates2011.fasta
CS_CladeB_Bayer2012.fasta          DS_CladeC_Ladner2012.fasta
CS_MonoBrev_King2008.fasta         DS_CladeD1_Gates2011.fasta
CS_StrainCCMP2430a_iMicrobe.fasta  DS_CladeD_Ladner2012.fasta
```

## 11-May-2016 - Merge individual blastdb for corals and symbionts, dirty and clean
Files have been merged, first all CC for the clean coral db, then CC and DC for the dirty coral db and the same for the symbionts. A new directory was created and the merged fasta files were moved into it.
```
[ysawall@d430-041 New_sequences]$ cat CC_* > CC_all_db.fasta
cat: CS_all_db.fasta: input file is output file
[ysawall@d430-041 New_sequences]$ cat CC_all_db.fasta DC_* > DC_all_db.fasta
cat: DC_all_db.fasta: input file is output file
[ysawall@d430-041 New_sequences]$ cat CS_* > CS_all_db.fasta
cat: CS_all_db.fasta: input file is output file
[ysawall@d430-041 New_sequences]$ cat CS_all_db.fasta DS_* > DS_all_db.fasta
cat: DS_all_db.fasta: input file is output file

[ysawall@d430-041 New_blast_dbs]$ pwd
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_blast_dbs
[ysawall@d430-041 New_blast_dbs]$ ls
CC_all_db.fasta  CS_all_db.fasta  DC_all_db.fasta  DS_all_db.fasta
```

load the blast module (blast/2.2.29) and format blastdbs into nucl format. the following arguments are needed for the makeblastdb command: -in INFILE.fasta -dbtype nucl -title DBTITLE -out DBNAME
Ignore error message during the run.
E.g. for clean corals
```
[ysawall@d430-041 New_blast_dbs]$ makeblastdb -in CC_all_db.fasta -dbtype nucl -out CC_all_nucldb
...
[ysawall@d430-041 New_blast_dbs]$ ls
CC_all_db.fasta    CC_all_nucldb.nin  CS_all_db.fasta  DS_all_db.fasta
CC_all_nucldb.nhr  CC_all_nucldb.nsq  DC_all_db.fasta
```

Problem with the second makeblastdb (dirty coral) with the following error messages towards the end. No nucl files were created.

```
[ysawall@d430-041 New_blast_dbs]$ makeblastdb -in DC_all_db.fasta -dbtype nucl -out DC_all_nucldb
...
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Title is very long: 1365 characters (max is 1000)
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Title is very long: 1086 characters (max is 1000)
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring FASTA modifier(s) found because the input was not expected to have any.
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Title is very long: 1005 characters (max is 1000)
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 64997560: 1119-1122, 1124-1125, 1127-1128, 1130-1132, 1135-1136, 1141-1143, 1145, 1147-1156, 1159, 1161-1162, 1164-1165, 1170, 1172-1192
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: First data line in seq is about 45% ambiguous nucleotides (shouldn't be over 40%)
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: First data line in seq is about 45% ambiguous nucleotides (shouldn't be over 40%)
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73470796: 2-8, 10-17, 19-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73470876: 2-8, 10, 14-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73470980: 2-8, 10-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471076: 2-8, 10-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471116: 2-8, 10-26, 29-30, 33, 37, 39, 42-45, 47-48, 50, 52, 59-61, 63, 70, 78-79, 81, 84
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471142: 2-8, 10-17, 19-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471368: 2-8, 10, 14-23, 25-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471384: 2-8, 10, 14-23, 25-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471400: 2-8, 10-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471450: 2-8, 10-17, 19-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471476: 2-8, 10-17, 19-21, 24-25, 28, 32, 34, 37-40, 42-43, 45, 47, 54-56, 58, 65, 73-74, 76, 79
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471482: 2-8, 10, 14-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471518: 2-8, 10, 14-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471566: 2-8, 10, 14-27, 30-31, 34, 38, 40, 43-46, 48-49, 51, 53, 60-62, 64, 71, 79-80, 82, 85
Error: (1431.1) FASTA-Reader: Warning: FASTA-Reader: Ignoring invalid residues at position(s): On line 73471574: 2-8, 10-11, 13-15

volume: DC_all_nucldb.00
volume: DC_all_nucldb.01

file: DC_all_nucldb.00.nin
file: DC_all_nucldb.00.nhr
file: DC_all_nucldb.00.nsq
file: DC_all_nucldb.01.nin
file: DC_all_nucldb.01.nhr
file: DC_all_nucldb.01.nsq
file: DC_all_nucldb.nal

Error: NCBI C++ Exception:
    "/home/coremake/release_build/build/PrepareRelease_Linux32-Centos_JSID_01_69_130.14.18.6_9056__PrepareRelease_Linux32-Centos_1386773752/c++/compilers/unix/../../src/objtools/blast/seqdb_writer/build_db.cpp", line 407: Error: BLASTDB::ncbi::s_FixBioseqDeltas() - Bioseq must have Seq-data or Delta containing only literals.
```

Clean symbionts (CS) nucl files. Both went fine.
```
[ysawall@d430-041 New_blast_dbs]$ makeblastdb -in CS_all_db.fasta -dbtype nucl -out CS_all_nucldb
....
Adding sequences from FASTA; added 403809 sequences in 40.5421 seconds.
[ysawall@d430-041 New_blast_dbs]$ makeblastdb -in DS_all_db.fasta -dbtype nucl -out DS_all_nucldb
...
Adding sequences from FASTA; added 747502 sequences in 70.3477 seconds.
```

Trouble shooting for DC sequences: take every DC sequence individually and run the makeblastdb command. Found the bad sequence and labelled it DCbad_P.... It was consequently excluded from the DC_all_db.fasta.
Strangely, however, all the nucl files of DC are now doubled: .00. and .01.  ??
And there is an additional file with the ending .nal  ??
```
[ysawall@d430-041 New_blast_dbs]$ makeblastdb -in DC_all_db.fasta -dbtype nucl -out DC_all_nucldb
...
Adding sequences from FASTA; added 3078441 sequences in 399.798 seconds.
[ysawall@turing1 New_blast_dbs]$ ls
CC_all_db.fasta    CS_all_nucldb.nsq     **DC_all_nucldb.01.nsq**
CC_all_nucldb.nhr  DC_all_db.fasta       **DC_all_nucldb.nal**
CC_all_nucldb.nin  **DC_all_nucldb.00.nhr**  DS_all_db.fasta
CC_all_nucldb.nsq  **DC_all_nucldb.00.nin**  DS_all_nucldb.nhr
CS_all_db.fasta    **DC_all_nucldb.00.nsq**  DS_all_nucldb.nin
CS_all_nucldb.nhr  **DC_all_nucldb.01.nhr**  DS_all_nucldb.nsq
CS_all_nucldb.nin  **DC_all_nucldb.01.nin**
```

## 12-May-2016 - Split assembly and do the blast
First, I tried a few more things to figure out what the probem was for havinghte double amount fo output files for DC after makeblastdb. Apparently the file is too big for one set of output files therefore two files are created. The nal file connects the two divided files again.
Then I split the assembly into 20000 bp pieces, after copying and adapting the dbparams.txt and copying the splitfasta.. script into my assembly directory.
```
[ysawall@d430-036 assembly]$ ls
dbparams.txt            Filtered_Trinity_over500.fasta
Filtered_Trinity.fasta  splitfasta_cluster_batchblast2dbs_advbioinf.py
[ysawall@d430-036 assembly]$ nano dbparams.txt
Dbpath  Databasename    Outfmt  NumThreads
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_blast_dbs/      CC_all_nucldb   5       2
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_blast_dbs/      DC_all_nucldb   5       2
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_blast_dbs/      CS_all_nucldb   5       2
/cm/shared/courses/dbarshis/RedSea/blastdbs/New_blast_dbs/      DS_all_nucldb   5       2
[ysawall@d430-036 assembly]$ ./splitfasta_cluster_batchblast2dbs_advbioinf.py  Filtered_Trinity_over500.fasta  20000 dbparams.txt
Traceback (most recent call last):
  File "./splitfasta_cluster_batchblast2dbs_advbioinf.py", line 78, in <module>
    db=cols[1]
IndexError: list index out of range
[ysawall@d430-036 assembly]$ ls
blastoutputs            Filtered_Trinity_over500.fasta                  submissionscripts
dbparams.txt            splitfasta_cluster_batchblast2dbs_advbioinf.py
Filtered_Trinity.fasta  splitfastas
[ysawall@d430-036 assembly]$ bash
[ysawall@d430-036 assembly]$ for i in submissionscripts/* ; do qsub $i ; done
Your job 129083 ("Filtered_Trinity_over500_000001-020000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129084 ("Filtered_Trinity_over500_000001-020000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129085 ("Filtered_Trinity_over500_000001-020000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129086 ("Filtered_Trinity_over500_000001-020000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129087 ("Filtered_Trinity_over500_020001-040000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129088 ("Filtered_Trinity_over500_020001-040000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129089 ("Filtered_Trinity_over500_020001-040000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129090 ("Filtered_Trinity_over500_020001-040000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129091 ("Filtered_Trinity_over500_040001-060000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129092 ("Filtered_Trinity_over500_040001-060000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129093 ("Filtered_Trinity_over500_040001-060000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129094 ("Filtered_Trinity_over500_040001-060000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129095 ("Filtered_Trinity_over500_060001-080000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129096 ("Filtered_Trinity_over500_060001-080000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129097 ("Filtered_Trinity_over500_060001-080000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129098 ("Filtered_Trinity_over500_060001-080000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129099 ("Filtered_Trinity_over500_080001-100000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129100 ("Filtered_Trinity_over500_080001-100000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129101 ("Filtered_Trinity_over500_080001-100000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129102 ("Filtered_Trinity_over500_080001-100000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129103 ("Filtered_Trinity_over500_100001-120000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129104 ("Filtered_Trinity_over500_100001-120000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129105 ("Filtered_Trinity_over500_100001-120000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129106 ("Filtered_Trinity_over500_100001-120000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129107 ("Filtered_Trinity_over500_120001-140000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129108 ("Filtered_Trinity_over500_120001-140000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129109 ("Filtered_Trinity_over500_120001-140000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129110 ("Filtered_Trinity_over500_120001-140000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129111 ("Filtered_Trinity_over500_140001-160000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129112 ("Filtered_Trinity_over500_140001-160000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129113 ("Filtered_Trinity_over500_140001-160000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129114 ("Filtered_Trinity_over500_140001-160000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129115 ("Filtered_Trinity_over500_160001-180000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129116 ("Filtered_Trinity_over500_160001-180000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129117 ("Filtered_Trinity_over500_160001-180000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129118 ("Filtered_Trinity_over500_160001-180000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129119 ("Filtered_Trinity_over500_180001-200000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129120 ("Filtered_Trinity_over500_180001-200000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129121 ("Filtered_Trinity_over500_180001-200000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129122 ("Filtered_Trinity_over500_180001-200000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129123 ("Filtered_Trinity_over500_200001-220000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129124 ("Filtered_Trinity_over500_200001-220000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129125 ("Filtered_Trinity_over500_200001-220000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129126 ("Filtered_Trinity_over500_200001-220000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129127 ("Filtered_Trinity_over500_220001-240000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129128 ("Filtered_Trinity_over500_220001-240000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129129 ("Filtered_Trinity_over500_220001-240000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129130 ("Filtered_Trinity_over500_220001-240000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129131 ("Filtered_Trinity_over500_240001-260000_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129132 ("Filtered_Trinity_over500_240001-260000_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129133 ("Filtered_Trinity_over500_240001-260000_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129134 ("Filtered_Trinity_over500_240001-260000_blastsub_DS_all_nucldb.sh") has been submitted
Your job 129135 ("Filtered_Trinity_over500_260001-264158_blastsub_CC_all_nucldb.sh") has been submitted
Your job 129136 ("Filtered_Trinity_over500_260001-264158_blastsub_CS_all_nucldb.sh") has been submitted
Your job 129137 ("Filtered_Trinity_over500_260001-264158_blastsub_DC_all_nucldb.sh") has been submitted
Your job 129138 ("Filtered_Trinity_over500_260001-264158_blastsub_DS_all_nucldb.sh") has been submitted
[ysawall@d430-036 assembly]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
 129062 500.00020 QRLOGIN    ysawall      r     05/12/2016 12:23:48 main@d430-036.cm.cluster           1   
 129083 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:07 main@c8-023.cm.cluster             2   
 129084 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:07 main@cr-046.cm.cluster             2   
 129085 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:07 main@cr-046.cm.cluster             2   
 129086 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:07 main@cr-046.cm.cluster             2   
 129087 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@d430-043.cm.cluster           2   
 129088 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-028.cm.cluster             2   
 129089 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-028.cm.cluster             2   
 129090 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-028.cm.cluster             2   
 129091 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-028.cm.cluster             2   
 129092 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-018.cm.cluster             2   
 129093 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-018.cm.cluster             2   
 129094 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-018.cm.cluster             2   
 129095 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-018.cm.cluster             2   
 129096 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:22 main@cr-080.cm.cluster             2   
 129097 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129098 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129099 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129100 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129101 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129102 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@cr-011.cm.cluster             2   
 129103 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@d430-005.cm.cluster           2   
 129104 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@d430-005.cm.cluster           2   
 129105 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@d430-005.cm.cluster           2   
 129106 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:37 main@d430-005.cm.cluster           2   
 129107 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-072.cm.cluster             2   
 129108 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-072.cm.cluster             2   
 129109 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-072.cm.cluster             2   
 129110 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-072.cm.cluster             2   
 129111 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-072.cm.cluster             2   
 129112 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-070.cm.cluster             2   
 129113 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-070.cm.cluster             2   
 129114 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-070.cm.cluster             2   
 129115 500.00019 Filtered_T ysawall      r     05/12/2016 12:42:52 main@cr-070.cm.cluster             2   
 129116 500.00019 Filtered_T ysawall      r     05/12/2016 12:43:07 main@c8-014.cm.cluster             2   
 129117 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@c8-014.cm.cluster             2   
 129118 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@c8-014.cm.cluster             2   
 129119 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@c8-014.cm.cluster             2   
 129120 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-040.cm.cluster             2   
 129121 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-040.cm.cluster             2   
 129122 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-034.cm.cluster             2   
 129123 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-034.cm.cluster             2   
 129124 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-034.cm.cluster             2   
 129125 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:07 main@cr-034.cm.cluster             2   
 129126 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-025.cm.cluster             2   
 129127 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129128 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129129 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129130 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129131 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129132 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@c8-036.cm.cluster             2   
 129133 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@d430-035.cm.cluster           2   
 129134 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:22 main@d430-026.cm.cluster           2   
 129135 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:37 main@c8-029.cm.cluster             2   
 129136 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:37 main@c8-029.cm.cluster             2   
 129137 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:37 main@c8-029.cm.cluster             2   
 129138 500.00018 Filtered_T ysawall      r     05/12/2016 12:43:37 main@c8-029.cm.cluster             2   
```

## 16-May-2016 - Parse blast outputs & Reparse parse outputs

Check blast output (example given below for DS)

```
[ysawall@turing1 DS_all_nucldb]$ pwd
/cm/shared/courses/dbarshis/RedSea/assembly/blastoutputs/DS_all_nucldb
[ysawall@turing1 DS_all_nucldb]$ ls
Filtered_Trinity_over500_000001-020000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_020001-040000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_040001-060000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_060001-080000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_080001-100000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_100001-120000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_120001-140000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_140001-160000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_160001-180000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_180001-200000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_200001-220000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_220001-240000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_240001-260000_blastx2DS_all_nucldb.xml
Filtered_Trinity_over500_260001-264158_blastx2DS_all_nucldb.xml
```

In each blastoutput directory (CC, CS, DC, DS) I made a qsub script for parsing the blastoutput files (see example below for DS)

```
[ysawall@turing1 DS_all_nucldb]$ nano DS_parse_script.sh

#! /bin/bash

#$ -cwd
#$ -o DS_parse.txt -j y
#$ -q main

module load biopython/1.64
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/parse_blastnortblastx_advbioinf.py DS_parse_output.txt blastn *.xml

[ysawall@turing1 DS_all_nucldb]$ qsub DS_parse_script.sh
Your job 130089 ("DS_parse_script.sh") has been submitted
```

Check, if all 4 jobs are running --> OK
```
[ysawall@turing1 DS_all_nucldb]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
 130086 500.00004 CC_parse_s ysawall      r     05/16/2016 11:35:08 main@cr-043.cm.cluster             1
 130087 500.00002 CS_parse_s ysawall      r     05/16/2016 11:37:38 main@cr-067.cm.cluster             1
 130088 500.00001 DC_parse_s ysawall      r     05/16/2016 11:38:53 main@c8-029.cm.cluster             1
 130089 500.00000 DS_parse_s ysawall      r     05/16/2016 11:40:23 main@cr-039.cm.cluster             1
```

Check the output of the parsing (example for CC)
```
[ysawall@turing1 CC_all_nucldb]$ ls
CC_parse_output.txt
CC_parse_script.sh
CC_parse.txt 
Filtered_Trinity_over500_000001-020000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_020001-040000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_040001-060000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_060001-080000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_080001-100000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_100001-120000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_120001-140000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_140001-160000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_160001-180000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_180001-200000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_200001-220000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_220001-240000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_240001-260000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_260001-264158_blastx2CC_all_nucldb.xml
```

Re-parse parsed blast outputs using qsub and the script ReParseBlastbycutoffs_advbioinf.py and checked output..
```
[ysawall@turing1 CC_all_nucldb]$ nano CC_reparse_script.sh

#! /bin/bash

#$ -cwd
#$ -o CC_ReParse.txt -j y
#$ -q main

module load biophyton/1.64
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 50per100bpmatch.txt lengthidentity 0.50 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 60per100bpmatch.txt lengthidentity 0.60 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 70per100bpmatch.txt lengthidentity 0.70 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 80per100bpmatch.txt lengthidentity 0.80 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 85per100bpmatch.txt lengthidentity 0.85 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 90per100bpmatch.txt lengthidentity 0.90 100 CC_parse_output.txt
/cm/shared/courses/dbarshis/15AdvBioinf/scripts/ReParseBlastbycutoffs_advbioinf.py 95per100bpmatch.txt lengthidentity 0.95 100 CC_parse_output.txt

[ysawall@turing1 CC_all_nucldb]$ qsub CC_reparse_script.sh

[ysawall@turing1 CC_all_nucldb]$ ls
CC_parse_output_50per100bpmatch.txt
CC_parse_output_60per100bpmatch.txt
CC_parse_output_70per100bpmatch.txt
CC_parse_output_80per100bpmatch.txt
CC_parse_output_85per100bpmatch.txt
CC_parse_output_90per100bpmatch.txt
CC_parse_output_95per100bpmatch.txt
CC_parse_output.txt
CC_parse_script.sh
CC_parse.txt
CC_reparse_script.sh
CC_ReParse.txt
Filtered_Trinity_over500_000001-020000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_020001-040000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_040001-060000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_060001-080000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_080001-100000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_100001-120000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_120001-140000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_140001-160000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_160001-180000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_180001-200000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_200001-220000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_220001-240000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_240001-260000_blastx2CC_all_nucldb.xml
Filtered_Trinity_over500_260001-264158_blastx2CC_all_nucldb.xml

[ysawall@turing1 CC_all_nucldb]$ less CC_ReParse.txt

Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
ModuleCmd_Load.c(208):ERROR:105: Unable to locate a modulefile for 'biophyton/1.64'
CC_parse_output.txt     0.50    100     Number of Good Hits:    116345
CC_parse_output.txt     0.50    100     Number of unique matches:       28795
CC_parse_output.txt     0.60    100     Number of Good Hits:    116345
CC_parse_output.txt     0.60    100     Number of unique matches:       28795
CC_parse_output.txt     0.70    100     Number of Good Hits:    110354
CC_parse_output.txt     0.70    100     Number of unique matches:       28610
CC_parse_output.txt     0.80    100     Number of Good Hits:    55042
CC_parse_output.txt     0.80    100     Number of unique matches:       17172
CC_parse_output.txt     0.85    100     Number of Good Hits:    22581
CC_parse_output.txt     0.85    100     Number of unique matches:       8287
CC_parse_output.txt     0.90    100     Number of Good Hits:    5613
CC_parse_output.txt     0.90    100     Number of unique matches:       2746
CC_parse_output.txt     0.95    100     Number of Good Hits:    2773
CC_parse_output.txt     0.95    100     Number of unique matches:       1686

[ysawall@turing1 CC_all_nucldb]$ less CC_parse_output_80per100bpmatch.txt

Query Name      Query Length    Subject Name    Subject Length  Alignment Length        Query Start     Query End       Subject Start   Subject End     Query Sequence  Subject Sequence        Hsp Score       Hsp Expect
      Hsp Identities  Percent Match   Number_of_gaps
TR34|c0_g1_i1 len=623 path=[601:0-622] [-1, 601, -2]    623     gnl|BL_ORD_ID|780545 comp270507_c0_seq1 len=422 path=[400:0-421]        422     294     336     623     112     405     CCTGTGTCTATGTTGCATGAACGTGGCGATGGATTGTCGATGACCTTACCATAGAGCCAAGGAGCCCCCCGTTGAGATGGGTGAGGCTTTGCATAAGTATATGAGCCTAACGGTAGTGGTAACAAAGGAGGTTGTGTATACTTGTCATATTAAGCTTTAGAGGCTCGTCTGCGGAGAGTAGTTTAGGAGCTGACTGTCAAAGGGTCCGCAGGGTCGGGCTTGAGTAGGTCTTCTGAAAGTGGCAGTGTAGAGT------GTCTGCCCATTAACCTCTGGGCTGGTGAGAAGGAG  CCTGTGTCTATGTTGTACGAATTTGGCGATGGCTTGTCGATGATCCGACCATAGAGCCAAGGAGCCCCCCGTTGAGATGGGCGAGGCTTTGCGTAAGCATGGGAGCCTAATGGCAGTGGCGACAGAGGAGGTTGTGCATACTTGTCATATTGAGATTTAGAGGCTTCTCTACGGAGAGTGATTCCGGAGCTGACTGTCGAAGGATCTGCAGGTTCAGGTTTGAGCAGGTTTTCTGAAAGTGGGAGTGTGGAGTGAGTACGTCTGCCCATCAACCTCTGGGCTGGGGAGAAGGAG  358.0   6.31884e-86     248     0.843537414966  6
TR83|c0_g1_i1 len=636 path=[614:0-635] [-1, 614, -2]    636     gnl|BL_ORD_ID|417091 s23Contig26993_11 [3 - 2333]       2331    592     1       592     592     1       GACCAAACAGTTTCATTTGCTCTGAAGGGACTTCGGTCATAGAATAGATCTGCATGCGAAGCATTTCCCATCCTTCACTAGGTTCGCATTCAAGCTCAAACTCTTTGCCACGATAGCGCACCAGAATAGGTATGCCACTGCCAACTTCGGGCAAACAGGCTGCATCCAAATCAATCGAGCGTGGCAAAGTGGAGACAAAATTTGGCGCCATGACTCTACTTCTCGCGTTGGTATCCAACACACCACCTGTGTGTGCATCCAGCAAAACTAAG

[ysawall@turing1 DC_all_nucldb]$ less DC_ReParse.txt

Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
ModuleCmd_Load.c(208):ERROR:105: Unable to locate a modulefile for 'biophyton/1.64'
DC_parse_output.txt     0.50    100     Number of Good Hits:    221009
DC_parse_output.txt     0.50    100     Number of unique matches:       112363
DC_parse_output.txt     0.60    100     Number of Good Hits:    221009
DC_parse_output.txt     0.60    100     Number of unique matches:       112363
DC_parse_output.txt     0.70    100     Number of Good Hits:    213355
DC_parse_output.txt     0.70    100     Number of unique matches:       110701
DC_parse_output.txt     0.80    100     Number of Good Hits:    166963
DC_parse_output.txt     0.80    100     Number of unique matches:       90378
DC_parse_output.txt     0.85    100     Number of Good Hits:    149531
DC_parse_output.txt     0.85    100     Number of unique matches:       83131
DC_parse_output.txt     0.90    100     Number of Good Hits:    134110
DC_parse_output.txt     0.90    100     Number of unique matches:       76955
DC_parse_output.txt     0.95    100     Number of Good Hits:    117094
DC_parse_output.txt     0.95    100     Number of unique matches:       70486

[ysawall@turing1 CS_all_nucldb]$ less CS_ReParse.txt

Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
ModuleCmd_Load.c(208):ERROR:105: Unable to locate a modulefile for 'biophyton/1.64'
CS_parse_output.txt     0.50    100     Number of Good Hits:    104155
CS_parse_output.txt     0.50    100     Number of unique matches:       67363
CS_parse_output.txt     0.60    100     Number of Good Hits:    104155
CS_parse_output.txt     0.60    100     Number of unique matches:       67363
CS_parse_output.txt     0.70    100     Number of Good Hits:    99696
CS_parse_output.txt     0.70    100     Number of unique matches:       65954
CS_parse_output.txt     0.80    100     Number of Good Hits:    74894
CS_parse_output.txt     0.80    100     Number of unique matches:       52381
CS_parse_output.txt     0.85    100     Number of Good Hits:    63515
CS_parse_output.txt     0.85    100     Number of unique matches:       44019
CS_parse_output.txt     0.90    100     Number of Good Hits:    58654
CS_parse_output.txt     0.90    100     Number of unique matches:       40512
CS_parse_output.txt     0.95    100     Number of Good Hits:    55834
CS_parse_output.txt     0.95    100     Number of unique matches:       39429

[ysawall@turing1 DS_all_nucldb]$ less DS_ReParse.txt

Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
in/bash: Command not found.
ModuleCmd_Load.c(208):ERROR:105: Unable to locate a modulefile for 'biophyton/1.64'
DS_parse_output.txt     0.50    100     Number of Good Hits:    130614
DS_parse_output.txt     0.50    100     Number of unique matches:       76064
DS_parse_output.txt     0.60    100     Number of Good Hits:    130614
DS_parse_output.txt     0.60    100     Number of unique matches:       76064
DS_parse_output.txt     0.70    100     Number of Good Hits:    125869
DS_parse_output.txt     0.70    100     Number of unique matches:       75188
DS_parse_output.txt     0.80    100     Number of Good Hits:    101481
DS_parse_output.txt     0.80    100     Number of unique matches:       69422
DS_parse_output.txt     0.85    100     Number of Good Hits:    95514
DS_parse_output.txt     0.85    100     Number of unique matches:       67575
DS_parse_output.txt     0.90    100     Number of Good Hits:    93146
DS_parse_output.txt     0.90    100     Number of unique matches:       66754
DS_parse_output.txt     0.95    100     Number of Good Hits:    89909
DS_parse_output.txt     0.95    100     Number of unique matches:       65664
```

## 17-May-2016 - generate "good coral" and "good symbiont" reference sequences
**Dan's advice:** In terms of what cutoffs to use to generate a "good coral" and a "good symbiont" reference sequence is really a matter of personal preference. There are 99696 contigs in the Clean Sym blast at a 70%/100bp cutoff and 149531 in the DC blast at an 85%/100bp cutoff. I'd start there and see how many are left after the symbiont sequences are filtered out. Then we can adjust the cutoffs if we need to include more or less sequences. We're really looking for <70K sequences in the end, but it depends on the sequencing, species, etc.
   * Used WinSCP to copy the files DC_parse_output_85per100bpmatch.txt and CS_parse_output_70per100bpmatch.txt on computer (D:/GEOMAR/Jeddah Daten/Transcriptomics/assembly_blast/) --> took 3 hours for the 2 files!!
**In R** we compared the two seqeunces with each other
<code bahs>
> setwd("D:/GEOMAR/Jeddah Daten/Transcriptomics/assembly_blast")
> dirtycoral<-read.delim("DC_parse_output_85per100bpmatch.txt")
> dim(dirtycoral)
[1] 149531     16
> cleansym<-read.delim("CS_parse_output_70per100bpmatch.txt")
> dim(cleansym)
[1] 99696    16
> View(cleansym)
> View(dirtycoral)
> sum(!(dirtycoral$Query.Name%in%cleansym$Query.Name))
[1] 112227
> write.table(dirtycoral[!(dirtycoral$Query.Name%in%cleansym$Query.Name), "Query.Name"], file="GoodCoralContig_112227.txt", quote = F, row.names = F)
```
   * open new file "GoodCoralContig_112227.txt" in editor and change header to "ContigName". Here are the first few lines
```
ContigName
TR72|c0_g1_i1 len=870 path=[1748:0-788 1749:789-808 1750:809-869] [-1, 1748, 1749, 1750, -2]
TR72|c0_g2_i1 len=875 path=[1745:0-788 1746:789-813 1747:814-874] [-1, 1745, 1746, 1747, -2]
TR140|c0_g1_i1 len=632 path=[1219:0-631] [-1, 1219, -2]
TR202|c0_g1_i1 len=1217 path=[2438:0-166 2439:167-190 2440:191-1216] [-1, 2438, 2439, 2440, -2]
TR223|c0_g1_i1 len=513 path=[1005:0-448 1006:449-512] [-1, 1005, 1006, -2]
TR309|c0_g1_i1 len=501 path=[1031:0-88 1032:89-112 1037:113-326 1035:327-350 1036:351-500] [-1, 1031, 1032, 1037, 1035, 1036, -2]
TR326|c0_g1_i1 len=780 path=[1540:0-262 1541:263-286 1542:287-779] [-1, 1540, 1541, 1542, -2]
```

## 18-May-2016 - generate "good coral" and "good symbiont" reference sequences
The GoodCoralContig_1112227 file has too many contigs. Try different scenarious for DC-CS and DS-CC..
Additional parse text files with differnt % cutoffs where copied to the computer and read into R. Than different combinations for the comparison of contig names were used...
```
> dirtycoral90<-read.delim("DC_parse_output_90per100bpmatch.txt")
> cleansym60<-read.delim("CS_parse_output_60per100bpmatch.txt")
> dirtysym85<-read.delim("DS_parse_output_85per100bpmatch.txt")
> dirtysym90<-read.delim("DS_parse_output_90per100bpmatch.txt")
> cleancoral70<-read.delim("CC_parse_output_70per100bpmatch.txt")
## #data table "dirtycoral" is "dirtycoral85" and "cleansym" is "cleansym70"
> sum(!(dirtycoral90$Query.Name%in%cleansym$Query.Name))
[1] 97806
> sum(!(dirtycoral90$Query.Name%in%cleansym60$Query.Name))
[1] 94829
> sum(!(dirtysym85$Query.Name%in%cleancoral70$Query.Name))
[1] 85356
> sum(!(dirtysym90$Query.Name%in%cleancoral70$Query.Name))
[1] 84403
## # and more combinations....
> dirtycoral95<-read.delim("DC_parse_output_95per100bpmatch.txt")
> cleansym50<-read.delim("CS_parse_output_50per100bpmatch.txt")
> dirtysym95<-read.delim("DS_parse_output_95per100bpmatch.txt")
> cleancoral60<-read.delim("CC_parse_output_60per100bpmatch.txt")
> cleancoral50<-read.delim("CC_parse_output_50per100bpmatch.txt")
> sum(!(dirtycoral95$Query.Name%in%cleansym60$Query.Name))
[1] 79276
> sum(!(dirtycoral95$Query.Name%in%cleansym50$Query.Name))
[1] 79276
> ## # cleansym50 and cleansym60 have the same number of contigs (stupid me...)
> sum(!(dirtysym90$Query.Name%in%cleancoral60$Query.Name))
[1] 82825
> sum(!(dirtysym95$Query.Name%in%cleancoral60$Query.Name))
[1] 79978
> sum(!(dirtysym95$Query.Name%in%cleancoral50$Query.Name))
[1] 79978
> ## # cleancoral50 and cleancoral60 have the same number of contigs (stupid me...)
```
Take the most conservative options:
   * for GoodCoralContig use dirtycoral95 vs cleansym60
   * for GoodSymbiontContig use dirtysym95 vs cleancoral60
```
> write.table(dirtycoral95[!(dirtycoral95$Query.Name%in%cleansym60$Query.Name), "Query.Name"], file="GoodCoralContig_95vs60_79276.txt", quote = F, row.names = F)
> write.table(dirtysym95[!(dirtysym95$Query.Name%in%cleancoral60$Query.Name), "Query.Name"], file="GoodSymbiontContig_95vs60_79978.txt", quote = F, row.names = F)
```
copy the Good...Contig files back into the cluster and place it in the fasta folder together with the Trinity .fasta files. Than run the script "getseqsfromfasta_advbioinf.py" to extract the good contigs from the Filtered_Trinity_over500.fasta file
```
[ysawall@turing1 fastas]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas
[ysawall@turing1 fastas]$ ls
Filtered_Trinity.fasta          GoodCoralContig_95vs60_79276.txt
Filtered_Trinity_over500.fasta  GoodSymbiontContig_95vs60_79978.txt
[ysawall@turing1 fastas]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/getseqsfromfasta_advbioinf.py GoodCoralContig_95vs60_79276.txt Filtered_Trinity_over500.fasta Assembly_79276ofSEQS_GoodCoral.fasta
[ysawall@turing1 fastas]$ ls
Assembly_79276ofSEQS_GoodCoral.fasta  GoodCoralContig_95vs60_79276.txt
Filtered_Trinity.fasta                GoodSymbiontContig_95vs60_79978.txt
Filtered_Trinity_over500.fasta
[ysawall@turing1 fastas]$ less Assembly_79276ofSEQS_GoodCoral.fasta
>TR309|c0_g1_i1 len=501 path=[1031:0-88 1032:89-112 1037:113-326 1035:327-350 1036:351-500] [-1, 1031, 1032, 1037, 1035, 1036, -2]
AACGAGAGGTGAAACCCCATCTCTTCGCACGCAGCAGGGCCTTCGCACCGAGGAGCTTTCCAACTTCCACAATGAAGGCTCACTTTGGTCCCTGCGAGGACCTTGGGGTGATTGTCGAGAAGCGGCCGCCTGGTGTGCCACTGGCCATAGTTTCACAAGATCTCCGACCTAGCACTGTGGGCGCTGCCTCGCAAAGGACAGGAACGCCCAGGGTCGAAACGACTTCAAGGCCAAGCACGACTGGAATCTCCAGCAGGTCACAGGTGAATACCATCGACAGGGTCGCAGGCGCGACATTGCCTGAGCTAATGAGGTCGAGGCATCCCTTGCTGGAAGTCAGCTTGCGAAGTGCGCGACTGACCCCCAGCCAAAGACCGCCTGCAGGGGCATAGCATGGTGGAGCCCGAGTCGCAGTGGAAGTGCCGCTGTACCAACGACTGCCCAAGCCGGACAGCCGCGTACACAGCGGCGGCCGTGGAAGAGAGACCAGTTTGGTGAAAG
>TR326|c0_g1_i1 len=780 path=[1540:0-262 1541:263-286 1542:287-779] [-1, 1540, 1541, 1542, -2]
TGAAGGGATTCGGATGCTGGAGCTCGAAAAAGCTCTGAAGAAGTTAGGCGGCGATGAATTGACAAAGAAGCAAAAGAGAGTTCTGGAGGATATGAGCCGGGGGATAGTGAACAAACTCCTGCATGGCCCAATGACAGCCCTCCGGTGCGATGGGACAGACCCCAAGGCTGTTGGCGAAACTCTTGCCAATATGGAAGCGTTGGAAAGGATGTTTGGGCTGCTGACCTCTGAACTCGGCTC
...
[ysawall@turing1 fastas]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/getseqsfromfasta_advbioinf.py GoodSymbiontContig_95vs60_79978.txt Filtered_Trinity_over500.fasta Assembly_79978ofSEQS_GoodSymbiont.fasta
[ysawall@turing1 fastas]$ ls
Assembly_79276ofSEQS_GoodCoral.fasta     Filtered_Trinity_over500.fasta
Assembly_79978ofSEQS_GoodSymbiont.fasta  GoodCoralContig_95vs60_79276.txt
Filtered_Trinity_over500.fasta
[ysawall@turing1 fastas]$ less Assembly_79978ofSEQS_GoodSymbiont.fasta
>TR16|c0_g1_i1 len=1638 path=[4999:0-1600 5000:1601-1637] [-1, 4999, 5000, -2]
TGGCTGTAATCGTGTGCGCTGCCCGATGATGCCTGGGCTGCCCGTGAGCCGATGTGGACTTGGGCTGGCGGAGCAACCTTGCTGGGAGGACTGCTGCTATGGCCACCAGTCAAACTGAGTCCAGAAGTTGTCATCATCAATGCATTGGTTTTAGTGCTGCTGTGCTACCGCTGTATCAGCAGAATGGTCTTTGCCGGAAAGGGGCATGTTTGGCACATCGCGCCATCTTCTATAGAGAAACTTGGATTGCTGGACTCGGCTAATGTGTGGATGGCATTGCTCTATGCCGCCAGCTCGCTGACATTGTTGGGCACTCTCCAGTTCTTCGTGATCGTTTCGCGGTTGTTACCTGACCTGTGGCAATTTCGCGATGCACATGCGGTTGGCGCGCAGATCATGAACGCGTTTCCAGCCGACTTGGAATTGAACATGACAAACGGCGAGCTGTTCAGCTCCCGCAAAAATCGCTTCAACATTGACCTGCCTTCATGGAGCTGGTTCGACATGTGTGATGGCACATGGAAGCTGAAACTGGCTTCTTTGGACTTCGGCTCACCTGACTTGTATGCGGTGGGTCGATTGCTGGCTATTGTGTATTTCAATCTGTCCCCTTCTTTGCAAGTGACTGATGTTAGCGTAGGCGAGGAGGTCGAGGTTCAGGTTGACAGCGACTTGATCGACTGCGGGGCGCGACGCTCGTGGTTGCCACTACCATTCAAAGGTAAGTGGGTACGAGCAGTGGTTCGGTCCGTGCAGCCTTCGACGCTCTTGTCTGAGTTCCGGTACATCGTGAGAGTCCAAGATGAGTGGAAAGCCTGTGCTGCAGATTCAATGAAGGAGCTCCTTCCCTGCGGCCCTGGTTTATTTCCCAACTGCTCTTGCGCGGTGTCGCCCACAAGCTTGAGACGAGCACAGCCGCGCATGGTTGTACTGGCTTCCGAAGAGGATGTGCTTGAAGACGTCTCCGAGTTGCGCGAGCTGCGGGCAGAGATGATCTTTGCACGCGAGAGGTTTGCAAATTTGGAAGGTTTTTCCTTCCATCACGGCCAGTTCTGGCGGTACAGGAACATCAAGGCCAGCGAGATGTGGCGAAGGTATTCCTTGAAGGAGCTGAGTGCTCATGGTCAGCTACAATGCATGACAGGGCTCTACTGCAACAGCGATGGCAAGAAGAACCTTCACTGCTCGCGTGTGGCAGCTACTGCAAATCTGAAGACATGGAGCAAAGAGTTCCCCCATCTGGCCGCCGTGGTGCAGTGGAACCTGCATGTACCCGTGCTTTGCATGCTTCTGTGGCTGGCTTGTGTTTCGGCAACCCTTCTCTGCCGTGGCTTCACCTTGCTGGCGTTGTACCTCCCAGCTGGATATGTTTCCTACGCATTGGTGAGGCACGTGGACACAGCGCTTCTGGCCCCGTCAGTTTCATTGTGCATGGTGCTGTTCACCGCTATGCCATTTCTGTACTTCTCGTGCGTTTGCGAGACGTTGCCGGAGCTTTGGGGACATGGGGAGCATTTGCCGCCTTGGCTGCAGACCGCGCTTTCGTTCGAAGTGCAGGGCGGTGCCTGCTCGTTCTGGCTGTGGCTTGCGTGGAGCAGCTAGATCGTTGTCCGCCGTCGACAACGTCGTTGCAGCCAG
>TR16|c0_g2_i1 len=2484 path=[4997:0-1600 4998:1601-2483] [-1, 4997, 4998, -2]
TGGCTGTAATCGTGTGCGCTGCCCGATGATGCCTGGGCTGCCCGTGAGCCGATGTGGACTTGGGCTGGCGGAGCAACCTT
```  
Check number of contigs again and get some statistics
```
[ysawall@turing1 fastas]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/avg_cov_len_fasta_advbioinf.py Assembly_79276ofSEQS_GoodCoral.fasta
The total number of sequences is 79276
The average sequence length is 1860
The total number of bases is 147505095
The minimum sequence length is 500
The maximum sequence length is 20312
The N50 is 2482
Median Length = 1183
contigs < 150bp = 0
contigs >= 500bp = 79276
contigs >= 1000bp = 53122
contigs >= 2000bp = 26293

[ysawall@turing1 fastas]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/avg_cov_len_fasta_advbioinf.py Assembly_79978ofSEQS_GoodSymbiont.fasta
The total number of sequences is 79978
The average sequence length is 1274
The total number of bases is 101914672
The minimum sequence length is 500
The maximum sequence length is 10892
The N50 is 1461
Median Length = 1057
contigs < 150bp = 0
contigs >= 500bp = 79978
contigs >= 1000bp = 43069
contigs >= 2000bp = 10468
```

Create a new dbparams.txt file for splitting and blasting the Assembly file
```
[ysawall@turing1 fastas]$ nano dbparams.txt
Databasename    Outfmt  NumThreads
/cm/shared/courses/apps/blast/databases/        nr      5       2
/cm/shared/courses/apps/blast/databases/        uniprot_sprot   7       2
/cm/shared/courses/apps/blast/databases/        uniprot_TrEMBL  7       2
```

## 19-May-2016 - combine "good coral" and "good symbiont" reference sequences, split & blast
Combine the two Assembly files
```
[ysawall@turing1 fastas]$ pwd
/cm/shared/courses/dbarshis/RedSqea/fastas
[ysawall@turing1 fastas]$ cat Assembly_79276ofSEQS_GoodCoral.fasta Assembly_79978ofSEQS_GoodSymbiont.fasta > Assembly_GoodCoralSymbiont.fasta
[ysawall@turing1 fastas]$ ls
Assembly_79276ofSEQS_GoodCoral.fasta     Filtered_Trinity.fasta
Assembly_79978ofSEQS_GoodSymbiont.fasta  Filtered_Trinity_over500.fasta
Assembly_GoodCoralSymbiont.fasta         GoodCoralContig_95vs60_79276.txt
BlastAssemblyGoodContig.sh               GoodSymbiontContig_95vs60_79978.txt
dbparams.txt
```

Split the joint Assembly file into 5000 contig pieces
```
[ysawall@turing1 scripts]$ pwd
/cm/shared/courses/dbarshis/15AdvBioinf/scripts
[ysawall@turing1 scripts]$ cp splitfasta_cluster_batchblast2dbs_blastx_advbioinf.py ../../RedSea/fastas/

[ysawall@turing1 fastas]$ ./splitfasta_cluster_batchblast2dbs_blastx_advbioinf.py Assembly_GoodCoralSymbiont.fasta 5000 dbparams.txt
[ysawall@turing1 fastas]$ ls ./splitfastas/
Assembly_GoodCoralSymbiont_000001-005000.fasta
Assembly_GoodCoralSymbiont_005001-010000.fasta
Assembly_GoodCoralSymbiont_010001-015000.fasta
Assembly_GoodCoralSymbiont_015001-020000.fasta
Assembly_GoodCoralSymbiont_020001-025000.fasta
Assembly_GoodCoralSymbiont_025001-030000.fasta
Assembly_GoodCoralSymbiont_030001-035000.fasta
Assembly_GoodCoralSymbiont_035001-040000.fasta
Assembly_GoodCoralSymbiont_040001-045000.fasta
Assembly_GoodCoralSymbiont_045001-050000.fasta
Assembly_GoodCoralSymbiont_050001-055000.fasta
Assembly_GoodCoralSymbiont_055001-060000.fasta
Assembly_GoodCoralSymbiont_060001-065000.fasta
Assembly_GoodCoralSymbiont_065001-070000.fasta
Assembly_GoodCoralSymbiont_070001-075000.fasta
Assembly_GoodCoralSymbiont_075001-080000.fasta
Assembly_GoodCoralSymbiont_080001-085000.fasta
Assembly_GoodCoralSymbiont_085001-090000.fasta
Assembly_GoodCoralSymbiont_090001-095000.fasta
Assembly_GoodCoralSymbiont_095001-100000.fasta
Assembly_GoodCoralSymbiont_100001-105000.fasta
Assembly_GoodCoralSymbiont_105001-110000.fasta
Assembly_GoodCoralSymbiont_110001-115000.fasta
Assembly_GoodCoralSymbiont_115001-120000.fasta
Assembly_GoodCoralSymbiont_120001-125000.fasta
Assembly_GoodCoralSymbiont_125001-130000.fasta
Assembly_GoodCoralSymbiont_130001-135000.fasta
Assembly_GoodCoralSymbiont_135001-140000.fasta
Assembly_GoodCoralSymbiont_140001-145000.fasta
Assembly_GoodCoralSymbiont_145001-150000.fasta
Assembly_GoodCoralSymbiont_150001-155000.fasta
Assembly_GoodCoralSymbiont_155001-159254.fasta
```

Submit blasting jobs (95 jobs in total)
```
[ysawall@turing1 fastas]$ for i in submissionscripts/* ; do qsub $i ; done
Your job 130511 ("Assembly_GoodCoralSymbiont_000001-005000_blastsub_nr.sh") has been submitted
Your job 130512 ("Assembly_GoodCoralSymbiont_000001-005000_blastsub_uniprot_sprot.sh") has been submitted
Your job 130513 ("Assembly_GoodCoralSymbiont_000001-005000_blastsub_uniprot_TrEMBL.sh") has been submitted
...
Your job 130604 ("Assembly_GoodCoralSymbiont_155001-159254_blastsub_nr.sh") has been submitted
Your job 130605 ("Assembly_GoodCoralSymbiont_155001-159254_blastsub_uniprot_sprot.sh") has been submitted
Your job 130606 ("Assembly_GoodCoralSymbiont_155001-159254_blastsub_uniprot_TrEMBL.sh") has been submitted

[ysawall@turing1 fastas]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID
-----------------------------------------------------------------------------------------------------------------
 130511 500.00002 Assembly_G ysawall      r     05/19/2016 06:21:32 main@d430-023.cm.cluster           2       
 130512 500.00002 Assembly_G ysawall      r     05/19/2016 06:21:32 main@d430-023.cm.cluster           2       
...
```

## 29/30-05-2016 - Total annotation and mapping 

Blasting results and combining result files for total annotation
```
[ysawall@turing1 nr]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/blastoutputs/nr
[ysawall@turing1 nr]$ ls
Assembly_GoodCoralSymbiont_000001-005000_blastx2nr.xml
Assembly_GoodCoralSymbiont_005001-010000_blastx2nr.xml
…
## #parse .xml files into one big .txt file
[ysawall@turing1 nr]$ nano Parse_nr_results.sh
#!/bin/bash

#$ -cwd
#$ -o 2016-05-29_ParseNRoutefile.txt -j y
#$ -q main
#$ -m beas
#$ -M ysawall@geomar.de

module load biopython/1.64

/cm/shared/courses/dbarshis/15AdvBioinf/scripts/parse_blastnortblastx_advbioinf.py All_nr_GoodCoralSym_blastx2nr.txt tblastx *.xml

[ysawall@turing1 uniprot_sprot]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/blastoutputs/uniprot_sprot
[ysawall@turing1 uniprot_sprot]$ ls
Assembly_GoodCoralSymbiont_000001-005000_blastx2uniprot_sprot.txt
Assembly_GoodCoralSymbiont_005001-010000_blastx2uniprot_sprot.txt
…
## #cat .txt files into one big .txt file
[ysawall@turing1 uniprot_sprot]$ cat *.txt > All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt
```

Make new directory called “totalannotation” and copy Assembly_*.fasta, All_nr_GoodCoralSym_blastx2nr.txt, All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt into it, as well as the file “stuffsfornr.txt”  from the15AdvBioinf/assignments_exercises/week10 directory
```
[ysawall@turing1 totalannotation]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation
[ysawall@turing1 totalannotation]$ ls
All_nr_GoodCoralSym_blastx2nr.txt         
All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt  
Assembly_79276ofSEQS_GoodCoral.fasta
Assembly_GoodCoralSymbiont.fasta
Assembly_79978ofSEQS_GoodSymbiont.fasta 
stuffsfornr.txt
```

Start totalannotation_advbioinf.py 
```
[ysawall@turing1 totalannotation]$ nano totalannotation.sh
#!/bin/bash

#$ -cwd
#$ -o 2016-05-29_totalannotationRoutfile.txt -j y
#$ -q main
#$ -m beas
#$ -M ysawall@geomar.de

/cm/shared/courses/dbarshis/15AdvBioinf/scripts/totalannotation_advbioinf.py Assembly_GoodCoralSymbiont.fasta All_nr_GoodCoralSym_blastx2nr.txt stuffsfornr.txt All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt  All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt 1e-4 flatfiles Assembly_GoodCoralSymbiont_totalannotated.txt

[ysawall@turing1 totalannotation]$ ls
2016-05-29_totalannotationRoutfile.txt          
All_nr_GoodCoralSym_blastx2nr.txt                
All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt  
Assembly_GoodCoralSymbiont.fasta
Assembly_GoodCoralSymbiont_totalannotated.txt
Flatfiles
stuffsfornr.txt
totalannotation.sh
```

Shorten names of contigs of GoodCoral and GoodSymbiont fasta files
(trim off everything in the name after the first space in the name and adds a suffix to each sequence name)
```
[ysawall@turing1 totalannotation]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation
[ysawall@turing1 totalannotation]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/trimfastanames_advbioinf.py Assembly_79276ofSEQS_GoodCoral.fasta coral
[ysawall@turing1 totalannotation]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/trimfastanames_advbioinf.py Assembly_79978ofSEQS_GoodSymbiont.fasta symbiont
## # new files: Assembly_79276ofSEQS_GoodCoral_shortnames.fasta, Assembly_79978ofSEQS_GoodSymbiont_shortnames.fasta
```

Combine *shortnames.fasta files
```
[ysawall@turing1 totalannotation]$ cat *shortnames.fasta > Assembly_GoodCoralSymbiont_formapping.fasta
```

mkdir “mapping” in “totalannotation” and cp “Assembly_GoodCoralSymbiont.fasta into “mapping” --> OK

mv all filtered fastq files (R1 only) in the mapping directory, as well
```
[ysawall@turing1 RedSea]$ mv ./2016-Feb_RawData/fastqs/QCFastqs/filtered/*_R1_*.fastq ./fastas/totalannotation/mapping/
```

**Mapping:** Dan's advise: "In terms of the mapping, I have not yet run the bowtie and RSEM protocol. The instructions are here (https://github.com/trinityrnaseq/trinityrnaseq/wiki/Trinity-Transcript-Quantification) and seem pretty straightforward, though I'm not sure if we have all the necessary programs currently installed on the cluster. If you can figure out what is installed and what needs to be installed you can email hpc@odu.edu and request additional programs to be installed (giving them the installation instructions and download location and explaining that you're working with me)."
 
However, for now, I used the "old" protocol
```
[ysawall@turing1 mapping]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation/mapping
[ysawall@turing1 mapping]$ nano mapping_fastqs.sh
#!/bin/bash

#$ -cwd
#$ -o 2016-05-30_mapping -j y
#$ -S /bin/bash
#$ -q main
#$ -m beasn
#$ -M ysawall@geomar.de
#$ -pe blast 4

/cm/shared/courses/dbarshis/15AdvBioinf/scripts/batchbwamem_advbioinf.py Assembly_GoodCoralSymbiont_formapping.fasta *.fastq
[ysawall@turing1 mapping]$ qsub mapping_fastqs.sh
Your job 133241 ("mapping_fastqs.sh") has been submitted
```

View mapping stats...
```
[ysawall@turing1 mapping]$ nano mappingstats.txt
10876325 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 secondary
169 + 0 supplimentary
0 + 0 duplicates
6837830 + 0 mapped (62.87%:-nan%)
0 + 0 paired in sequencing
0 + 0 read1
0 + 0 read2
0 + 0 properly paired (-nan%:-nan%)
0 + 0 with itself and mate mapped
0 + 0 singletons (-nan%:-nan%)
0 + 0 with mate mapped to a different chr
0 + 0 with mate mapped to a different chr (mapQ>=5)
Stats for: 2011-DOG-10_R1_clippedtrimmedfilterd
9920607 + 0 in total (QC-passed reads + QC-failed reads)
0 + 0 secondary
57343 + 0 supplimentary
0 + 0 duplicates
6525168 + 0 mapped (65.77%:-nan%)
....
```
View annotation output
```
[ysawall@turing1 totalannotation]$ less 2016-05-29_totalannotationRoutfile.txt
Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
Read in fasta of 157386 sequences: ...
Read in nr blast...
Number of good nr matches: 183
Number not matched in nr: 157203
Searching for badwords...
Number of nr hits with only a bad word hit: 44
Number of nr hits with a good word hit: 139
Read in swissprot blast ...
Number of good swissprot matches: 68209
Read in TrEMBL blast ...
Number of repeat matches from TrEMBL: 68209
Number of additional good matches from TrEMBL: 0
flatfilesneeded: 22809
downloading flat files ...
extracting relevant info from flat files ...
don't worry this takes awhile ...
Hits not matched in sprot: 89354
compiling extracted information ...
...
```

## 31-05-2016 - sequence counts 
start qrsh session
mkdir "samfiles" and mv all sam files in there
summarize the expression counts from the sam files usiing the scirpt "countxpression_advbioinf.py"
```
[ysawall@turing1 samfiles]$ qrsh
[ysawall@cr-043 samfiles]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation/mapping/samfiles
[ysawall@cr-043 samfiles]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/countxpression_advbioinf.py 20 20 summarystats.txt *.sam
```
view summary file (output)
```
[ysawall@turing1 samfiles]$ cat summarystats.txt
Filename        Total#Reads     NumContigsMatched       NumUnaligned    NumAligned      NumMultiAligned NumSingleAligned        NumQualSingles  PropQualAligned
2011-DOG-10_R1_clippedtrimmedfilterd.sam        10876325        66837   4038495 6837830 0       6837830 2956758 0.272
2011-DOG-3_R1_clippedtrimmedfilterd.sam 9920607 71292   3395439 6525168 0       6525168 2982936 0.301
2011-DOG-6_R1_clippedtrimmedfilterd.sam 55554743        86460   18496652        37058091        0       37058091        16177150        0.291
2011-DOG-7_R1_clippedtrimmedfilterd.sam 11410172        71301   3850306 7559866 0       7559866 3227562 0.283
2011-DOG-8_R1_clippedtrimmedfilterd.sam 11556094        65092   4376358 7179736 0       7179736 2616113 0.226
2011-DOG-9_R1_clippedtrimmedfilterd.sam 10580066        65985   3979036 6601030 0       6601030 2709857 0.256
2011-MAQ-1_R1_clippedtrimmedfilterd.sam 8394627 90781   2902042 5492585 0       5492585 2677421 0.319
2011-MAQ-2_R1_clippedtrimmedfilterd.sam 12001180        94017   3876672 8124508 0       8124508 3838958 0.320
2011-MAQ-3_R1_clippedtrimmedfilterd.sam 8127757 67533   2669612 5458145 0       5458145 2380656 0.293
2011-MAQ-4_R1_clippedtrimmedfilterd.sam 9417227 74657   3557845 5859382 0       5859382 2489466 0.264
2011-MAQ-5_R1_clippedtrimmedfilterd.sam 12750330        68194   4639412 8110918 0       8110918 3385906 0.266
2011-MAQ-6_R1_clippedtrimmedfilterd.sam 13221885        74214   4461992 8759893 0       8759893 3991807 0.302
2011-WAJ-2_R1_clippedtrimmedfilterd.sam 10905126        69914   4063601 6841525 0       6841525 3291871 0.302
2011-WAJ-3_R1_clippedtrimmedfilterd.sam 9814380 65194   3761012 6053368 0       6053368 2927796 0.298
2011-WAJ-4_R1_clippedtrimmedfilterd.sam 8991566 69685   3255958 5735608 0       5735608 2968374 0.330
2011-WAJ-7_R1_clippedtrimmedfilterd.sam 11105470        65806   4117583 6987887 0       6987887 3135616 0.282
2011-WAJ-8_R1_clippedtrimmedfilterd.sam 18289711        75315   7183110 11106601        0       11106601        5058563 0.277
2011-WAJ-9_R1_clippedtrimmedfilterd.sam 12931321        71933   4953566 7977755 0       7977755 3470966 0.268
2011-YAN-1_R1_clippedtrimmedfilterd.sam 11265468        71978   3709688 7555780 0       7555780 3405416 0.302
2011-YAN-2_R1_clippedtrimmedfilterd.sam 14229564        75370   4762177 9467387 0       9467387 4547409 0.320
2011-YAN-3_R1_clippedtrimmedfilterd.sam 13291678        69444   4866643 8425035 0       8425035 3381858 0.254
2011-YAN-4_R1_clippedtrimmedfilterd.sam 11024881        70962   3615030 7409851 0       7409851 3193874 0.290
2011-YAN-5_R1_clippedtrimmedfilterd.sam 11634208        68753   4405779 7228429 0       7228429 3103159 0.267
2011-YAN-6_R1_clippedtrimmedfilterd.sam 9291139 65803   3577581 5713558 0       5713558 2546425 0.274
2012-DOG-1_R1_clippedtrimmedfilterd.sam 9311600 43772   3387422 5924178 0       5924178 2036710 0.219
2012-DOG-2_R1_clippedtrimmedfilterd.sam 17409262        60159   5657104 11752158        0       11752158        4400716 0.253
2012-DOG-3_R1_clippedtrimmedfilterd.sam 7205329 51299   2358011 4847318 0       4847318 1810282 0.251
2012-DOG-4_R1_clippedtrimmedfilterd.sam 10952356        41635   4368762 6583594 0       6583594 2346170 0.214
2012-DOG-6_R1_clippedtrimmedfilterd.sam 10107573        51106   3776940 6330633 0       6330633 2209952 0.219
2012-DOG-7_R1_clippedtrimmedfilterd.sam 8875697 48633   3033122 5842575 0       5842575 2194191 0.247
2012-MAQ-1_R1_clippedtrimmedfilterd.sam 14610137        78608   5107011 9503126 0       9503126 4033479 0.276
2012-MAQ-2_R1_clippedtrimmedfilterd.sam 16445143        95687   5606483 10838660        0       10838660        4717244 0.287
2012-MAQ-3_R1_clippedtrimmedfilterd.sam 7034100 71759   2797739 4236361 0       4236361 1684062 0.239
2012-MAQ-4_R1_clippedtrimmedfilterd.sam 11748468        88120   4495336 7253132 0       7253132 2888087 0.246
2012-MAQ-5_R1_clippedtrimmedfilterd.sam 8744566 66697   3229044 5515522 0       5515522 2194919 0.251
2012-MAQ-6_R1_clippedtrimmedfilterd.sam 12238813        94463   4305511 7933302 0       7933302 3499916 0.286
2012-WAJ-4_R1_clippedtrimmedfilterd.sam 20562010        76717   7621777 12940233        0       12940233        5324657 0.259
2012-WAJ-5_R1_clippedtrimmedfilterd.sam 13925299        55040   5165238 8760061 0       8760061 2984587 0.214
2012-WAJ-6_R1_clippedtrimmedfilterd.sam 6759514 59724   2612961 4146553 0       4146553 1584673 0.234
2012-WAJ-7_R1_clippedtrimmedfilterd.sam 13739957        74094   4735180 9004777 0       9004777 4101136 0.298
2012-WAJ-8_R1_clippedtrimmedfilterd.sam 15701400        73294   5482729 10218671        0       10218671        4148024 0.264
2012-WAJ-9_R1_clippedtrimmedfilterd.sam 12952217        76582   4439613 8512604 0       8512604 3824719 0.295
2012-YAN-1_R1_clippedtrimmedfilterd.sam 10332826        69819   3402115 6930711 0       6930711 2904062 0.281
2012-YAN-2_R1_clippedtrimmedfilterd.sam 15530604        67785   5756879 9773725 0       9773725 3620008 0.233
2012-YAN-3_R1_clippedtrimmedfilterd.sam 5884343 65361   1998111 3886232 0       3886232 1772378 0.301
2012-YAN-4_R1_clippedtrimmedfilterd.sam 44940378        77676   16507911        28432467        0       28432467        10720464        0.239
2012-YAN-5_R1_clippedtrimmedfilterd.sam 32387855        71600   11807184        20580671        0       20580671        7229460 0.223
2012-YAN-6_R1_clippedtrimmedfilterd.sam 10644644        61471   3836690 6807954 0       6807954 2437041 0.229
```

## =====01-06-2016 – prepare sequence counts for analyses in R## =
Take file with sequence names only from the GoodCoralSymbiont fasta file (used for mapping)
```
[ysawall@cr-046 mapping]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation/mapping
[ysawall@cr-046 mapping]$ grep '>' Assembly_GoodCoralSymbiont_formapping.fasta | cut -d '>' -f 2 > sequencenames.txt
```
Add the header “contig” to sequencenames.txt file
```
[ysawall@cr-046 mapping]$ nano sequencenames.txt
Contig
TR309|c0_g1_i1_coral
TR326|c0_g1_i1_coral
TR328|c0_g1_i1_coral
….
```
Combine individual count files into one big .txt file using the script “ParseExpression2BigTable_advbioinf.py”
```
[ysawall@cr-046 mapping]$ mv sequencenames.txt ./samfiles/
[ysawall@cr-046 samfiles]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation/mapping/samfiles
[ysawall@cr-046 samfiles]$ /cm/shared/courses/dbarshis/15AdvBioinf/scripts/ParseExpression2BigTable_advbioinf.py sequencenames.txt Allcountsout.txt nomatch *_counts.txt
[ysawall@cr-046 samfiles]$ less Allcountsout.txt
Contig  2011-DOG-10_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads  2011-DOG-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-DOG-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-DOG-7_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-DOG-8_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-DOG-9_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-1_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-5_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-MAQ-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-7_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-8_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-WAJ-9_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-1_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-5_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2011-YAN-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-DOG-1_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-DOG-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-DOG-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-DOG-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-DOG-6_R1_clippedtrimmedfilterd_counAllcountsout.txt
ts.txt_UniqueTotReads   2012-DOG-7_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-1_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-5_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-MAQ-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-5_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-7_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-8_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-WAJ-9_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-1_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-2_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-3_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-4_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-5_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads   2012-YAN-6_R1_clippedtrimmedfilterd_counts.txt_UniqueTotReads
TR100002|c0_g1_i1_symbiont      131     135     667     109     72      111     54      135     73      95      129     125     153     149     185     121     158     110     179     277     127     110     159     140     2       5       1       0       5       1       131     149     3       64      84      79      168     15      44      227     101     188     115     128     99      240     89      51
TR100003|c0_g1_i1_symbiont      17      24      123     22      13      21      11      41      7       11      22      27      24      27      30      18      13      12      28      45      22      20      23      22      0       1       0       0       0       0       34      47      1       12      17      27      24      1       9       38      16      22      21      19      16      36      16      13
TR100003|c0_g2_i1_symbiont      0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0
TR100005|c0_g1_i1_symbiont      0       0       0       0       0       0       54      21      0       1       0       1       1       0       0       0       0       0       1       0       1       0       0       0       0       0       0       0       0       0       0       7       29      44      1       68      0       0       0       0       1       0       0       0       0       0       0       0
TR100007|c0_g1_i1_symbiont      0       0       0       0       0       0       4       2       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       0       1       3       3       0       3       0       0       0       0       0       1       0       0       0       0       0       0
....
```
transfer Allcountsout.txt to own computer (WinSCP)

## =====03-06-2016 – prepare sequence counts for analyses in R## =
Installed R and RStudio
Installed DESeq2
```
source("https://bioconductor.org/biocLite.R")
biocLite("DESeq2")
```
installed gplots by going to "Tools -> Install packages" in the RStudio Manager

Read in Allcountsout.txt to R, made condition table in Excel (saved as tab delimited .txt file) and read in condition.txt to R,
made sure, that the sample names are the same in the count and condition data frames.
```
> setwd("/Desktop/Transcriptomics - Red Sea")
> countTable<-read.delim("Allcountsout.txt")
> conds<-read.delim("conditions.txt")
#Didn't work for analyses, because I forgot to "describe" different components of tables
> rm(conds)
> rm(countTable)
> countTable<-read.delim("Allcountsout.txt", header = TRUE, stringsAsFactors = TRUE, row.names = 1)
> conds<-read.delim("conditions.txt", header = TRUE, stringsAsFactors = TRUE, row.names = 1)
> head(conds)
            season site position season_site
2011-DOG-10 summer  DOG        4       S-DOG
2011-DOG-3  summer  DOG        4       S-DOG
2011-DOG-6  summer  DOG        4       S-DOG
2011-DOG-7  summer  DOG        4       S-DOG
2011-DOG-8  summer  DOG        4       S-DOG
2011-DOG-9  summer  DOG        4       S-DOG
> colnames(countTable)
 [1] "X2011.DOG.10" "X2011.DOG.3"  "X2011.DOG.6" 
 [4] "X2011.DOG.7"  "X2011.DOG.8"  "X2011.DOG.9" 
 [7] "X2011.MAQ.1"  "X2011.MAQ.2"  "X2011.MAQ.3" 
...
#sample names don't match, therefore rename colnames of countTable with rownames of conds
> colnames(countTable)<-rownames(conds)
> colnames(countTable)
 [1] "2011-DOG-10" "2011-DOG-3"  "2011-DOG-6" 
 [4] "2011-DOG-7"  "2011-DOG-8"  "2011-DOG-9" 
 [7] "2011-MAQ-1"  "2011-MAQ-2"  "2011-MAQ-3" 
...
> dim(countTable)
[1] 159254     48
```

## =====06-06-2016 – run DESeq analyses in R## =
Run statistics with DESeq2
```
> dds <- DESeqDataSetFromMatrix(countData=countTable, colData=conds, design=~ site)
> dds<-DESeq(dds)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 2563 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing
```

**check for differences btw sites in winter**

```
#I defined the samples of Maqna (W-MAQ) as the "control treatment", since these featured the coolest conditions
> dds$season_site<-relevel(dds$season_site, "W-MAQ")
#Than I picked the relevant subset of samples 
> dds<-dds[,dds$season == "winter"]
#checked, whether we got the right samples (-> yes)
> as.data.frame(colData(dds))
           season site position season_site sizeFactor replaceable
2012-DOG-1 winter  DOG        4       W-DOG  0.8183474        TRUE
2012-DOG-2 winter  DOG        4       W-DOG  1.8271171        TRUE
2012-DOG-3 winter  DOG        4       W-DOG  0.6818513        TRUE
2012-DOG-4 winter  DOG        4       W-DOG  0.6400667        TRUE
2012-DOG-6 winter  DOG        4       W-DOG  0.8125522        TRUE
2012-DOG-7 winter  DOG        4       W-DOG  0.9137214        TRUE
2012-MAQ-1 winter  MAQ        1       W-MAQ  1.4495741        TRUE
2012-MAQ-2 winter  MAQ        1       W-MAQ  1.6504444        TRUE
2012-MAQ-3 winter  MAQ        1       W-MAQ  0.5087735        TRUE
2012-MAQ-4 winter  MAQ        1       W-MAQ  0.8775219        TRUE
2012-MAQ-5 winter  MAQ        1       W-MAQ  0.7460687        TRUE
2012-MAQ-6 winter  MAQ        1       W-MAQ  1.0234065        TRUE
2012-WAJ-4 winter  WAJ        2       W-WAJ  1.7115414        TRUE
2012-WAJ-5 winter  WAJ        2       W-WAJ  1.2702157        TRUE
2012-WAJ-6 winter  WAJ        2       W-WAJ  0.5760086        TRUE
2012-WAJ-7 winter  WAJ        2       W-WAJ  1.2702497        TRUE
2012-WAJ-8 winter  WAJ        2       W-WAJ  1.4703215        TRUE
2012-WAJ-9 winter  WAJ        2       W-WAJ  1.2085361        TRUE
2012-YAN-1 winter  YAN        3       W-YAN  1.0382052        TRUE
2012-YAN-2 winter  YAN        3       W-YAN  1.3571407        TRUE
2012-YAN-3 winter  YAN        3       W-YAN  0.5713525        TRUE
2012-YAN-4 winter  YAN        3       W-YAN  4.1318941        TRUE
2012-YAN-5 winter  YAN        3       W-YAN  2.8405464        TRUE
2012-YAN-6 winter  YAN        3       W-YAN  0.9524215        TRUE

> dds<-DESeq(dds)
using pre-existing size factors
estimating dispersions
found already estimated dispersions, replacing these
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing

#check overall result
> res<-results(dds)
> summary(res)
out of 125054 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 26064, 21% 
LFC < 0 (down)   : 4017, 3.2% 
outliers [1]     : 1158, 0.93% 
low counts [2]   : 35476, 28% 
(mean count < 1)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results
```

do individual comparisons between sites

```
> res<-results(dds, contrast=c("site", "MAQ", "WAJ"))
> summary(res)
out of 125054 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 8970, 7.2% 
LFC < 0 (down)   : 497, 0.4% 
outliers [1]     : 1158, 0.93% 
low counts [2]   : 49583, 40% 
(mean count < 2)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results
#order results according to padj (adjusted p-value) and check out which are the most differently expressed genes (lowest padj)
> resOrdered<-res[order(res$padj),]
> head(resOrdered)
log2 fold change (MAP): site MAQ vs WAJ 
Wald test p-value: site MAQ vs WAJ 
DataFrame with 6 rows and 6 columns
                            baseMean log2FoldChange     lfcSE      stat       pvalue         padj
                           <numeric>      <numeric> <numeric> <numeric>    <numeric>    <numeric>
TR106289|c0_g1_i1_symbiont 182.03053      7.6670596 1.0849447  7.066775 1.585759e-12 1.178425e-07
TR81198|c0_g1_i1_symbiont  182.07308      7.2092614 1.1100742  6.494396 8.336712e-11 3.097631e-06
TR154359|c3_g1_i1_symbiont  32.20793     -3.5912992 0.5793702 -6.198626 5.695835e-10 1.410915e-05
TR112519|c0_g1_i1_symbiont  40.26856      5.2326290 0.8761841  5.972066 2.342682e-09 4.352292e-05
TR129751|c1_g1_i1_coral    451.03858      0.7578686 0.1277225  5.933713 2.961595e-09 4.401700e-05
TR78315|c0_g1_i1_coral     756.15307      0.8537919 0.1454211  5.871170 4.327307e-09 5.359586e-05

#count number of differently expressed genes (padj<0.1 and 0.05)
> sum(res$padj<0.1, na.rm=T)
[1] 9467
> sum(res$padj<0.05, na.rm=T)
[1] 4093

#write significant results (sigres) into a new data frame, check some stats values and order sigres table again
> sigres<-res[res$padj < 0.05 & !is.na(res$padj),]
> mean(sigres$baseMean)
[1] 24.45978
> mean(sigres$log2FoldChange)
[1] 5.345404
> max(sigres$log2FoldChange)
[1] 8.141566
> min(sigres$padj)
[1] 1.178425e-07
> sigresOrdered<-sigres[order(sigres$padj),]
> head(sigresOrdered)
log2 fold change (MAP): site MAQ vs WAJ 
Wald test p-value: site MAQ vs WAJ 
DataFrame with 6 rows and 6 columns
                            baseMean log2FoldChange     lfcSE      stat       pvalue         padj
                           <numeric>      <numeric> <numeric> <numeric>    <numeric>    <numeric>
TR106289|c0_g1_i1_symbiont 182.03053      7.6670596 1.0849447  7.066775 1.585759e-12 1.178425e-07
TR81198|c0_g1_i1_symbiont  182.07308      7.2092614 1.1100742  6.494396 8.336712e-11 3.097631e-06
TR154359|c3_g1_i1_symbiont  32.20793     -3.5912992 0.5793702 -6.198626 5.695835e-10 1.410915e-05
TR112519|c0_g1_i1_symbiont  40.26856      5.2326290 0.8761841  5.972066 2.342682e-09 4.352292e-05
TR129751|c1_g1_i1_coral    451.03858      0.7578686 0.1277225  5.933713 2.961595e-09 4.401700e-05
TR78315|c0_g1_i1_coral     756.15307      0.8537919 0.1454211  5.871170 4.327307e-09 5.359586e-05

```
Realized that, if I compare every group with every group I will have a lot of tables...
Maybe this is not so useful. Therefore make a heat map.

**make a count table that is scaled by size factors**
re-run statistics with all data (both seasons)
```
> dds<-DESeqDataSetFromMatrix(countData = countTable, colData = conds, design = ~ season_site)
> dds<-DESeq(dds)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
> res<-results(dds)
```

prepare data for heatmap

```
> temp = t(sizeFactors(dds))
> sizematrix<-matrix(data=temp, nrow=nrow(countTable), ncol=ncol(temp), byrow=TRUE)
> scaledcounts = countsTable/sizematrix
> head(scaledcounts)
> genes4heatmap<-res[res$padj<0.05 & !is.na(res$padj),]
> dim(genes4heatmap)
[1] 6617    6

> head(genes4heatmap)
log2 fold change (MAP): season_site W-YAN vs S-DOG 
Wald test p-value: season_site W-YAN vs S-DOG 
DataFrame with 6 rows and 6 columns
                            baseMean log2FoldChange     lfcSE      stat       pvalue        padj
                           <numeric>      <numeric> <numeric> <numeric>    <numeric>   <numeric>
TR100036|c0_g2_i1_symbiont  18.50198     -1.8523844 0.4458050 -4.155145 3.250813e-05 0.002464860
TR100047|c0_g1_i1_coral    173.23507      0.5845062 0.1589377  3.677580 2.354576e-04 0.008398331
TR100082|c0_g1_i1_coral     16.21283      1.0332635 0.3464406  2.982513 2.858925e-03 0.035943438
TR100110|c0_g1_i1_symbiont  12.76961     -1.7626139 0.6062344 -2.907479 3.643545e-03 0.041191982
TR100138|c0_g1_i3_symbiont   7.70603     -1.2718245 0.4201985 -3.026723 2.472201e-03 0.033056484
TR100138|c0_g3_i1_symbiont  68.97808     -2.1043998 0.6381445 -3.297685 9.748540e-04 0.019335050

> data4heatmap<-scaledcounts[row.names(scaledcounts)%in%row.names(genes4heatmap),]
> dim(data4heatmap)
[1] 6617   48
> head(data4heatmap)
                           2011-DOG-10 2011-DOG-3 2011-DOG-6 2011-DOG-7 2011-DOG-8 2011-DOG-9 2011-MAQ-1
TR100036|c0_g2_i1_symbiont    30.54937  12.040827  208.25654  24.997393  23.383113  16.416382   6.208720
TR100047|c0_g1_i1_coral      114.86564  64.582616  916.62208 223.414199 209.217322 171.824801  71.745209
TR100082|c0_g1_i1_coral       13.44172   9.851585   58.66381  12.498696   8.614831  14.227531   6.898578
...
> temp = as.matrix(rowMeans(data4heatmap))
> head(temp)
                                 [,1]
TR100036|c0_g2_i1_symbiont  20.764708
TR100047|c0_g1_i1_coral    187.640377
TR100082|c0_g1_i1_coral     16.576248
TR100110|c0_g1_i1_symbiont  14.679194
TR100138|c0_g1_i3_symbiont   8.455897
TR100138|c0_g3_i1_symbiont  73.370987

> scaledmatrix<-matrix(data = temp, nrow = nrow(data4heatmap), ncol = ncol(data4heatmap), byrow = FALSE)
> data4heatmapscaled = data4heatmap/scaledmatrix
> head(data4heatmapscaled)
                           2011-DOG-10 2011-DOG-3 2011-DOG-6 2011-DOG-7 2011-DOG-8 2011-DOG-9 2011-MAQ-1
TR100036|c0_g2_i1_symbiont   1.4712161  0.5798698  10.029350  1.2038403  1.1260988  0.7905906  0.2990035
TR100047|c0_g1_i1_coral      0.6121585  0.3441829   4.884994  1.1906510  1.1149910  0.9157134  0.3823549
TR100082|c0_g1_i1_coral      0.8109027  0.5943194   3.539028  0.7540124  0.5197093  0.8583083  0.4161725
TR100110|c0_g1_i1_symbiont   1.9146434  0.7084105  10.090889  1.5964811  1.0899080  2.1621309  0.2349781
TR100138|c0_g1_i3_symbiont   1.7341388  0.3883517   8.672027  0.7390521  1.0187956  1.0354199  0.4079152
TR100138|c0_g3_i1_symbiont   2.3816282  0.6564353   7.715663  1.2989134  0.7883557  1.0441427  0.4325069

> dim(data4heatmapscaled)
[1] 6617   48
```

create heat maps

```
> library(gplots)

Attaching package: ‘gplots’

The following object is masked from ‘package:IRanges’:

    space

The following object is masked from ‘package:S4Vectors’:

    space

The following object is masked from ‘package:stats’:

    lowess

> pairs.breaks<-seq(0, 3.0, by=0.1)
> length(pairs.breaks)
[1] 31

> head(pairs.breaks)
[1] 0.0 0.1 0.2 0.3 0.4 0.5

> mycol<-colorpanel(n=30, low="black", high="yellow")

> pdf(file="X_byrow.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaled), Rowv = TRUE, Colv = FALSE, dendrogram = c("row"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = ("white"), sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

> pdf(file = "X_bycolumn.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaled), Rowv = TRUE, Colv = TRUE, dendrogram = c("col"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = "white", sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

#IMPORTANT to finish the plot (pdf document) by running dev.off at the end!! Otherwise the pdf can not be opened.

```
## =====07&08-06-2016 – run DESeq analyses in R## =
**Assess similarity between samples**
rlog-transform data to decrease dominance of strongly expressed genes
```
> rld<-rlog(dds)
> install.packages("devtools")
> library(devtools)
> install_github("vqv/ggbiplot")

# could't figure out how to run ggbiplot, and didn't like PCA created by DESeq. Therefore made similarity matrix and copied into excel and used PRIMERv6 to do PCA plots.
> sampleDists<-dist(t(assay(old)))
# (t stands for transpose)

```

make subsets of countTable data.frame for symbionts and corals only
```
# it took me a while to figure this out, mainly because of a stupid mistake: forgot the comma and space at the end of the entry, between brackets. This is important to gain the subset as a data.frame and not as "values" in R.

> countTableSym<-countTable[grep("symbiont", rownames(countTable)), ]
> countTableCor<-countTable[grep("coral", rownames(countTable)), ]
> dim(countTable)
[1] 159254     48
> dim(countTableSym)
[1] 79978    48
> dim(countTableCor)
[1] 79276    48

```
conduct DESeq with countTableSym and countTableCor and do all treatment sets (season, sites, season_site). 
```
# Symbionts

> ddsSymSeasonSite<-DESeqDataSetFromMatrix(countData = countTableSym, colData = conds, design = ~ season_site)
> ddsSymSeason<-DESeqDataSetFromMatrix(countData = countTableSym, colData = conds, design = ~ season)
> ddsSymSite<-DESeqDataSetFromMatrix(countData = countTableSym, colData = conds, design = ~ site)
> ddsSymSeasonSite<-DESeq(ddsSymSeasonSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing
> ddsSymSeason<-DESeq(ddsSymSeason)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 20216 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing

> ddsSymSite<-DESeq(ddsSymSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 12176 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing

#Corals

> ddsCorSeasonSite<-DESeqDataSetFromMatrix(countData = countTableCor, colData = conds, design = ~ season_site)
> ddsCorSeason<-DESeqDataSetFromMatrix(countData = countTableCor, colData = conds, design = ~ season)
> ddsCorSite<-DESeqDataSetFromMatrix(countData = countTableCor, colData = conds, design = ~ site)
> ddsCorSeasonSite<-DESeq(ddsCorSeasonSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing

> ddsCorSeason<-DESeq(ddsCorSeason)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 2288 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing

> ddsCorSite<-DESeq(ddsCorSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 2799 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing

#Combined Symbionts and Corals (I already ran DESeq for SeasonSite, but not for only Season and Site)

> ddsSeason<-DESeqDataSetFromMatrix(countData = countTable, colData = conds, design = ~ season)
> ddsSite<-DESeqDataSetFromMatrix(countData = countTable, colData = conds, design = ~ site)
> ddsSeason<-DESeq(ddsSeason)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 18510 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing

> ddsSite<-DESeq(ddsSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
-- replacing outliers and refitting for 2563 genes
-- DESeq argument 'minReplicatesForReplace' = 7 
-- original counts are preserved in counts(dds)
estimating dispersions
fitting model and testing
```

rlog transform data and created matrixes with SymSeasonSite and CorSeasonSite

```
> rldSym<-rlog(ddsSymSeasonSite)
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
> sampleDistsSym<-dist(t(assay(rldSym)))
> rldCor<-rlog(ddsCorSeasonSite)
> sampleDistsCor<-dist(t(assay(rldCor)))
```

**__Comparisons between sites__**
```
# just noticed that I had to re-run DESeq for all - symbionts and corals combined - since "dds" had been overwritten 
> ddsSeasonSite<-DESeqDataSetFromMatrix(countData = countTable, colData = conds, design = ~ season_site)
> ddsSeasonSite<-DESeq(ddsSeasonSite)
# OK, now ready to do comparisons

# between the most northern and the most southern site (MAQ vs DOG) 
# across season with combined data set (symbiont and coral contigs)
> resSiteMAQ_DOG<-results(ddsSite, contrast = c("site", "MAQ", "DOG"))
> summary(resSiteMAQ_DOG)
out of 129719 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 18719, 14% 
LFC < 0 (down)   : 2757, 2.1% 
outliers [1]     : 0, 0% 
low counts [2]   : 39883, 31% 
(mean count < 1)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results
> resSiteMAQ_DOG<-resSiteMAQ_DOG[order(resSiteMAQ_DOG$padj),]
> head(resSiteMAQ_DOG)
log2 fold change (MAP): site MAQ vs DOG 
Wald test p-value: site MAQ vs DOG 
DataFrame with 6 rows and 6 columns
                             baseMean log2FoldChange     lfcSE      stat       pvalue
                            <numeric>      <numeric> <numeric> <numeric>    <numeric>
TR81198|c0_g1_i1_symbiont  138.293971       9.109687 0.9694573  9.396687 5.630803e-21
TR106289|c0_g1_i1_symbiont 121.871671       8.883411 0.9536346  9.315319 1.215866e-20
TR54154|c0_g1_i1_symbiont   39.308956       5.777593 0.6754291  8.553959 1.189376e-17
TR82209|c0_g1_i1_symbiont   92.036718       8.500780 1.0005931  8.495742 1.966727e-17
TR7281|c0_g1_i1_symbiont     7.761995       4.831202 0.5924052  8.155232 3.485111e-16
TR146200|c3_g6_i5_symbiont  91.707880       8.983727 1.1106962  8.088375 6.046610e-16
                                   padj
                              <numeric>
TR81198|c0_g1_i1_symbiont  5.065583e-16
TR106289|c0_g1_i1_symbiont 5.469088e-16
TR54154|c0_g1_i1_symbiont  3.566621e-13
TR82209|c0_g1_i1_symbiont  4.423267e-13
TR7281|c0_g1_i1_symbiont   6.270551e-12
TR146200|c3_g6_i5_symbiont 9.066086e-12
> sum(resSiteMAQ_DOG$padj<0.1, na.rm=T)
[1] 21476
> sum(resSiteMAQ_DOG$padj<0.05, na.rm=T)
[1] 16088
> sigresSiteMAQ_DOG<-resSiteMAQ_DOG[resSiteMAQ_DOG$padj < 0.05 & !is.na(resSiteMAQ_DOG$padj),]
> mean(sigresSiteMAQ_DOG$log2FoldChange)
[1] 3.862274
> max(sigresSiteMAQ_DOG$log2FoldChange)
[1] 9.109687
> sigresSiteMAQ_DOG<-sigresSiteMAQ_DOG[order(sigresSiteMAQ_DOG$padj),]
> plotDispEsts(ddsSite, ylim=c(1e-6, 1e2))
#write csv file of sigres...
> sigresSiteMAQ_DOG <- as.data.frame(sigresSiteMAQ_DOG)
> write.csv(sigresSiteMAQ_DOG, file="sigresSiteMAQ_DOG.csv")




```

## =====09-06-2016 – run DESeq analyses in R## =
**Heat maps again for all contigs and for coral and symbionts separately**
Note: I reorganized the order of the samples, from north to south, therefore I had to start again with the DESeq analyses...

# SYMBIONTS
```

> countTableSym<-countTable[, c(7:24, 1:6, 31:48, 25:30)]
> conds<-conds[c(7:24, 1:6, 31:48, 25:30), ]

> ddsSymSeasonSite <- DESeqDataSetFromMatrix(countData=countTableSym, colData=conds, design=~ season_site)
> ddsSymSeasonSite<-DESeq(ddsSymSeasonSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing
> resSymSeasonSite<-results(ddsSymSeasonSite)

> temp = t(sizeFactors(ddsSymSeasonSite))
> sizematrixSySeSi<-matrix(data=temp, nrow=nrow(countTableSym), ncol=ncol(temp), byrow=TRUE)
> scaledcountsSySeSi = countTableSym/sizematrixSySeSi
> genes4heatmapSySeSi<-resSymSeasonSite[resSymSeasonSite$padj<0.05 & !is.na(resSymSeasonSite$padj),]
> data4heatmapSySeSi<-scaledcountsSySeSi[row.names(scaledcountsSySeSi)%in%row.names(genes4heatmapSySeSi),]
> dim(data4heatmapSySeSi)
[1] 10482    48
> temp = as.matrix(rowMeans(data4heatmapSySeSi))
> scaledmatrixSySeSi<-matrix(data = temp, nrow = nrow(data4heatmapSySeSi), ncol = ncol(data4heatmapSySeSi), byrow = FALSE)
> data4heatmapscaledSySeSi = data4heatmapSySeSi/scaledmatrixSySeSi
> pairs.breaks<-seq(0, 3.0, by=0.1)
> mycol<-colorpanel(n=30, low="black", high="yellow")

> pdf(file="CountsSym_byrow.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledSySeSi), Rowv = TRUE, Colv = FALSE, dendrogram = c("row"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = ("white"), sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

> pdf(file = "CountsSym_bycolumn.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledSySeSi), Rowv = TRUE, Colv = TRUE, dendrogram = c("col"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = "white", sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

```

# CORALS

```
countTableCor<-countTableCor[, c(7:24, 1:6, 31:48, 25:30)]

> ddsCorSeasonSite <- DESeqDataSetFromMatrix(countData=countTableCor, colData=conds, design=~ season_site)
> ddsCorSeasonSite<-DESeq(ddsCorSeasonSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
-- note: fitType='parametric', but the dispersion trend was not well captured by the
   function: y = a/x + b, and a local regression fit was automatically substituted.
   specify fitType='local' or 'mean' to avoid this message next time.
final dispersion estimates
fitting model and testing
> resCorSeasonSite<-results(ddsCorSeasonSite)

> temp = t(sizeFactors(ddsCorSeasonSite))
> sizematrixCoSeSi<-matrix(data=temp, nrow=nrow(countTableCor), ncol=ncol(temp), byrow=TRUE)
> scaledcountsCoSeSi = countTableCor/sizematrixCoSeSi
> genes4heatmapCoSeSi<-resCorSeasonSite[resCorSeasonSite$padj<0.05 & !is.na(resCorSeasonSite$padj),]
> data4heatmapCoSeSi<-scaledcountsCoSeSi[row.names(scaledcountsCoSeSi)%in%row.names(genes4heatmapCoSeSi),]
> dim(data4heatmapCoSeSi)
[1] 848  48

> temp = as.matrix(rowMeans(data4heatmapCoSeSi))
> scaledmatrixCoSeSi<-matrix(data = temp, nrow = nrow(data4heatmapCoSeSi), ncol = ncol(data4heatmapCoSeSi), byrow = FALSE)
> data4heatmapscaledCoSeSi = data4heatmapCoSeSi/scaledmatrixCoSeSi
> pairs.breaks<-seq(0, 3.0, by=0.1)
> mycol<-colorpanel(n=30, low="black", high="yellow")

> pdf(file="CountsCor_byrow.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledCoSeSi), Rowv = TRUE, Colv = FALSE, dendrogram = c("row"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = ("white"), sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

> pdf(file = "CountsCor_bycolumn.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledCoSeSi), Rowv = TRUE, Colv = TRUE, dendrogram = c("col"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = "white", sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

```

# Combined SYBMIONTS and CORALS

```
> countTable<-countTable[, c(7:24, 1:6, 31:48, 25:30)]
> ddsSeasonSite <- DESeqDataSetFromMatrix(countData=countTable, colData=conds, design=~ season_site)
> ddsSeasonSite<-DESeq(ddsSeasonSite)
estimating size factors
estimating dispersions
gene-wise dispersion estimates
mean-dispersion relationship
final dispersion estimates
fitting model and testing
> resSeasonSite<-results(ddsSeasonSite)
> temp = t(sizeFactors(ddsSeasonSite))
> sizematrixSeSi<-matrix(data=temp, nrow=nrow(countTable), ncol=ncol(temp), byrow=TRUE)
> scaledcountsSeSi = countTable/sizematrixSeSi
> genes4heatmapSeSi<-resSeasonSite[resSeasonSite$padj<0.05 & !is.na(resSeasonSite$padj),]
> data4heatmapSeSi<-scaledcountsSeSi[row.names(scaledcountsSeSi)%in%row.names(genes4heatmapSeSi),]
> dim(data4heatmapSeSi)
[1] 6617   48

> temp = as.matrix(rowMeans(data4heatmapSeSi))
> scaledmatrixSeSi<-matrix(data = temp, nrow = nrow(data4heatmapSeSi), ncol = ncol(data4heatmapSeSi), byrow = FALSE)
> data4heatmapscaledSeSi = data4heatmapSeSi/scaledmatrixSeSi
> pairs.breaks<-seq(0, 3.0, by=0.1)
> mycol<-colorpanel(n=30, low="black", high="yellow")

> pdf(file="CountsAll_byrow.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledSeSi), Rowv = TRUE, Colv = FALSE, dendrogram = c("row"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = ("white"), sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()

> pdf(file = "CountsAll_bycolumn.pdf",7,7)
> heatmap.2(data.matrix(data4heatmapscaledSeSi), Rowv = TRUE, Colv = TRUE, dendrogram = c("col"), scale = "none", keysize = 1, breaks = pairs.breaks, col = mycol, trace = "none", symkey = FALSE, density.info = "density", colsep = c(24), sepcolor = "white", sepwidth = c(.1,.1), margins = c(10,10), labRow = FALSE)
> dev.off()
```

Statistical Results of DESeq
```
> summary(resSeasonSite)

out of 129845 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 1725, 1.3% 
LFC < 0 (down)   : 9241, 7.1% 
outliers [1]     : 1377, 1.1% 
low counts [2]   : 63552, 49% 
(mean count < 3)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results

> summary(resCorSeasonSite)

out of 59890 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 649, 1.1% 
LFC < 0 (down)   : 690, 1.2% 
outliers [1]     : 1389, 2.3% 
low counts [2]   : 21910, 37% 
(mean count < 1)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results

> summary(resSymSeasonSite)

out of 69955 with nonzero total read count
adjusted p-value < 0.1
LFC > 0 (up)     : 2848, 4.1% 
LFC < 0 (down)   : 9955, 14% 
outliers [1]     : 14757, 21% 
low counts [2]   : 14750, 21% 
(mean count < 1)
[1] see 'cooksCutoff' argument of ?results
[2] see 'independentFiltering' argument of ?results
```

## === 04-11-2016 – Re-Annotation of TREMBLE blasting result ## =
After TrEMBL bla-sting was finished, results were annotated...

# combine all TrEMBLE.txt files into one big file
```
[ysawall@turing1 uniprot_TrEMBL]$ pwd
/cm/shared/courses/dbarshis/RedSea/fastas/blastoutputs/uniprot_TrEMBL
[ysawall@turing1 uniprot_TrEMBL]$ cat *uniprot_TrEMBL.txt > All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt
[ysawall@turing1 uniprot_TrEMBL]$ ls
All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt
Assembly_GoodCoralSymbiont_000001-005000_blastx2uniprot_TrEMBL.txt
Assembly_GoodCoralSymbiont_005001-010000_blastx2uniprot_TrEMBL.txt
...

# cp All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt into "totalannotation" dir
# run total annotation 
[ysawall@turing1 fastas]$ cp ./blastoutputs/uniprot_TrEMBL/All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt ./totalannotation/
[ysawall@turing1 totalannotation]$ ls
2016-05-29_totalannotationRoutfile.txt
All_nr_GoodCoralSym_blastx2nr.txt
All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt
All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt
Assembly_79276ofSEQS_GoodCoral.fasta
Assembly_79276ofSEQS_GoodCoral_shortnames.fasta
Assembly_79978ofSEQS_GoodSymbiont.fasta
Assembly_79978ofSEQS_GoodSymbiont_shortnames.fasta
Assembly_GoodCoralSymbiont.fasta
Assembly_GoodCoralSymbiont_formapping.fasta
Assembly_GoodCoralSymbiont_totalannotated.txt
flatfiles
mapping
stuffsfornr.txt
totalannotation.sh
#!/bin/bash

#$ -cwd
#$ -o 2016-05-29_totalannotationRoutfile.txt -j y
#$ -q main
#$ -m beas
#$ -M ysawall@geomar.de

/cm/shared/courses/dbarshis/15AdvBioinf/scripts/totalannotation_advbioinf.py Assembly_GoodCoralSymbiont.fasta All_nr_GoodCoralSym_blastx2nr.txt stuffsfornr.txt All_sprot_GoodCoralSym_blastx2uniprot_sprot.txt All_TrEMBL_GoodCoralSym_blastx2uniprot_TrEMBL.txt 1e-4 flatfiles Assembly_GoodCoralSymbiont_totalannotated.txt

[ysawall@turing1 totalannotation]$ qsub totalannotation.sh 
Your job 214169 ("totalannotation.sh") has been submitted
[ysawall@turing1 totalannotation]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
 214169 500.00000 totalannot ysawall      r     11/04/2016 15:17:30 main@coreV2-25-knc-006.cm.clus     1        


```

====Do mapping again with different script===

__Dan's advice:__ 

remap the reads against the coral and sym reference (as one file) using Misha's protocol (https://github.com/z0on/tag-based_RNAseq; bowtie2 for mapping and his countreads.pl script). I think his scripts take into account the multiply mapping reads and toss them out prior to counting for expression. Bowtie2 is available on the cluster (module load bowtie2/2.2.4) and you can download his countreads.pl script and should be able to run it. 
Let me know if you can get started based on Misha's instructions in the readme file. You'll need to make a seq2iso file to input to his countreads.pl script to combine the different "transcripts" into single "genes". Check out the trinity documentation https://github.com/trinityrnaseq/trinityrnaseq/wiki for the specifics (https://github.com/trinityrnaseq/trinityrnaseq/wiki/Output-of-Trinity-Assembly) but I think the file should look something like this:
TR3|c0_g1_i1    TR3_c0_g1
TR12|c0_g1_i1   TR12_c0_g1
TR1924|c0_g1_i1 TR1924_c0_g1
TR1924|c0_g1_i2 TR1924_c0_g1

Where you give each contig a "gene" name. In the above example the counts for TR1924|c0_g1_i1 and TR1924|c0_g1_i2 would be summed together (since they are both isoforms of TR1924|c0_g1) into one count for TR1924_c0_g1. I've taken out the "|" symbols in the second column because they cause problems with grep-ing and other command line functions. You should be able to make this table easily in excel by starting with a single column of all the sequence names and pulling out just the names up to "_g1"

## =====07-11-2016 – Mapping (Mikhail Matz protocol)## =
mkdir Bowtie2_mapping and cp all sample fast files in there, as well as the  Assembly_GoodCoralSymbiont_formappim.fasta --> **Done**
download Mikhail's scripts from github
```
[ysawall@turing1 Bowtie2_mapping]$ pwd
/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping
[ysawall@turing1 Bowtie2_mapping]$ mkdir scripts
[ysawall@turing1 Bowtie2_mapping]$ module load git/2.8.3
[ysawall@turing1 scripts]$ git clone https://github.com/z0on/tag-based_RNAseq.git
[ysawall@turing1 scripts]$ ls ./tag-based_RNAseq/
countreads.pl               launcher_creator.py      samcount_launch_bt2.pl
dna.mixing.R                mix_illumina_qpcr.R      samcount_launch.pl
expression_compiler.pl      ngs_concat.pl            samcount.pl
illumina_mix_data.csv       picogreen.csv            samcount_v.0.1.pl
iRNAseq_bowtie2map.pl       picogreen.R              selectFastaByHeader.pl
iRNAseq_shrimpmap_SAM.pl    README.md                splitFastaByHeader.pl
iRNAseq_trim_launch0.pl     rnaseq_clipper0.pl       tag_based_RNAseq_protocol.pdf
iRNAseq_trim_launch_bgi.pl  rnaseq_clipper_fasta.pl  tagseq_oligo_order.xls
iRNAseq_trim_launch.pl      rnaseq_clipper_old.pl    tagSeq_processing_README.txt
isogroup_namer.pl           rnaseq_clipper.pl        tag-seq_scripts_manual.pdf
```

create bowtie2 index for Assembly and test bowtie2 

```
module load bowtie2/2.2.4
[ysawall@turing1 Bowtie2_mapping]$ bowtie2-build Assembly_GoodCoralSymbiont_formapping.fasta Assembly_GoodCoralSymbiont_formapping 
#new files:
Assembly_GoodCoralSymbiont_formapping.1.bt2
Assembly_GoodCoralSymbiont_formapping.2.bt2
Assembly_GoodCoralSymbiont_formapping.3.bt2
Assembly_GoodCoralSymbiont_formapping.4.bt2
Assembly_GoodCoralSymbiont_formapping.rev.1.bt2
Assembly_GoodCoralSymbiont_formapping.rev.2.bt2

[ysawall@turing1 Bowtie2_mapping]$ bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-10_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam --no-unal 
10876156 reads; of these:
  10876156 (100.00%) were unpaired; of these:
    3662345 (33.67%) aligned 0 times
    2777232 (25.54%) aligned exactly 1 time
    4436579 (40.79%) aligned >1 times
66.33% overall alignment rate
```

compare first 10 lines of 2011-DOG-10 results from old mapping (batchbwamem)and from new mapping (Bowtie2)

```
**#batchbwamem**
[ysawall@turing1 samfiles]$ head 2011-DOG-10_R1_clippedtrimmedfilterd.sam
@SQ	SN:TR309|c0_g1_i1_coral	LN:501
@SQ	SN:TR326|c0_g1_i1_coral	LN:780
@SQ	SN:TR328|c0_g1_i1_coral	LN:812
@SQ	SN:TR470|c1_g1_i1_coral	LN:533
@SQ	SN:TR588|c1_g1_i1_coral	LN:508
@SQ	SN:TR610|c0_g1_i1_coral	LN:680
@SQ	SN:TR673|c0_g1_i1_coral	LN:529
@SQ	SN:TR711|c0_g1_i1_coral	LN:899
@SQ	SN:TR768|c0_g1_i1_coral	LN:500
@SQ	SN:TR775|c0_g1_i1_coral	LN:509

**#Botwie2**
[ysawall@turing1 Bowtie2_mapping]$ head 2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam 
@HD	VN:1.0	SO:unsorted
@SQ	SN:TR309|c0_g1_i1_coral	LN:501
@SQ	SN:TR326|c0_g1_i1_coral	LN:780
@SQ	SN:TR328|c0_g1_i1_coral	LN:812
@SQ	SN:TR470|c1_g1_i1_coral	LN:533
@SQ	SN:TR588|c1_g1_i1_coral	LN:508
@SQ	SN:TR610|c0_g1_i1_coral	LN:680
@SQ	SN:TR673|c0_g1_i1_coral	LN:529
@SQ	SN:TR711|c0_g1_i1_coral	LN:899
@SQ	SN:TR768|c0_g1_i1_coral	LN:500

**#--> same**
```

After running botwie2 with one sample sequence successfully, I wrote and submitted a qsub script. 

```
[ysawall@turing1 Bowtie2_mapping]$ nano bt2mapping.sh 
#! /bin/bash

#$ -cwd
#$ -o bt2mapping.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de

module load bowtie2/2.2.4

bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U *.fastq -S *bt2.sam --no-unal -k 5

[ysawall@turing1 Bowtie2_mapping]$ qsub bt2mapping.sh 
```
Did not work. Try again with only one sample file (2011-DOG-10_R1_clippedtrimmedfilterd.fastq)
```
[ysawall@turing1 Bowtie2_mapping]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
 214752 500.00000 bt2mapping ysawall      r     11/07/2016 15:00:56 main@coreV3-23-023.cm.cluster      1        
```
Worked fine, therefore try again with the other sample files, however, this time list every sample file separated by a comma.

```
[ysawall@turing1 Bowtie2_mapping]$ nano bt2mapping_all.sh
#! /bin/bash
 
#$ -cwd
#$ -o bt2mapping.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de
 
module load bowtie2/2.2.4

bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-3_R1_clippedtrimmedfilterd.fastq,2011-DOG-6_R1_clippedtrimmedfilterd.fastq,2011-DOG-7_R1_clippedtrimmedfilterd.fastq,2011-DOG-8_R1_clippedtrimmedfilterd.fastq,2011-DOG-9_R1_clippedtrimmedfilterd.fastq,2011-MAQ-1_R1_clippedtrimmedfilterd.fastq,2011-MAQ-2_R1_clippedtrimmedfilterd.fastq,2011-MAQ-3_R1_clippedtrimmedfilterd.fastq,2011-MAQ-4_R1_clippedtrimmedfilterd.fastq,2011-MAQ-5_R1_clippedtrimmedfilterd.fastq,2011-MAQ-6_R1_clippedtrimmedfilterd.fastq,2011-WAJ-2_R1_clippedtrimmedfilterd.fastq,2011-WAJ-3_R1_clippedtrimmedfilterd.fastq,2011-WAJ-4_R1_clippedtrimmedfilterd.fastq,2011-WAJ-7_R1_clippedtrimmedfilterd.fastq,2011-WAJ-8_R1_clippedtrimmedfilterd.fastq,2011-WAJ-9_R1_clippedtrimmedfilterd.fastq,2011-YAN-1_R1_clippedtrimmedfilterd.fastq,2011-YAN-2_R1_clippedtrimmedfilterd.fastq,2011-YAN-3_R1_clippedtrimmedfilterd.fastq,2011-YAN-4_R1_clippedtrimmedfilterd.fastq,2011-YAN-5_R1_clippedtrimmedfilterd.fastq,2011-YAN-6_R1_clippedtrimmedfilterd.fastq,2012-DOG-1_R1_clippedtrimmedfilterd.fastq,2012-DOG-2_R1_clippedtrimmedfilterd.fastq,2012-DOG-3_R1_clippedtrimmedfilterd.fastq,2012-DOG-4_R1_clippedtrimmedfilterd.fastq,2012-DOG-6_R1_clippedtrimmedfilterd.fastq,2012-DOG-7_R1_clippedtrimmedfilterd.fastq,2012-MAQ-1_R1_clippedtrimmedfilterd.fastq,2012-MAQ-2_R1_clippedtrimmedfilterd.fastq,2012-MAQ-3_R1_clippedtrimmedfilterd.fastq,2012-MAQ-4_R1_clippedtrimmedfilterd.fastq,2012-MAQ-5_R1_clippedtrimmedfilterd.fastq,2012-MAQ-6_R1_clippedtrimmedfilterd.fastq,2012-WAJ-4_R1_clippedtrimmedfilterd.fastq,2012-WAJ-5_R1_clippedtrimmedfilterd.fastq,2012-WAJ-6_R1_clippedtrimmedfilterd.fastq,2012-WAJ-7_R1_clippedtrimmedfilterd.fastq,2012-WAJ-8_R1_clippedtrimmedfilterd.fastq,2012-WAJ-9_R1_clippedtrimmedfilterd.fastq,2012-YAN-1_R1_clippedtrimmedfilterd.fastq,2012-YAN-2_R1_clippedtrimmedfilterd.fastq,2012-YAN-3_R1_clippedtrimmedfilterd.fastq,2012-YAN-4_R1_clippedtrimmedfilterd.fastq,2012-YAN-5_R1_clippedtrimmedfilterd.fastq,2012-YAN-6_R1_clippedtrimmedfilterd.fastq -S *_bt2.sam --no-unal -k 5

[ysawall@turing1 Bowtie2_mapping]$ qsub bt2mapping_all.sh
[ysawall@turing1 Bowtie2_mapping]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
 214754 500.00000 bt2mapping ysawall      r     11/07/2016 15:15:11 main@coreV3-23-033.cm.cluster      1        

```
Did not work. Try again tomorrow...

Prepare isoform tab table 

```
[ysawall@turing1 Bowtie2_mapping]$ grep ">" Assembly_GoodCoralSymbiont_formapping.fasta | perl -pe 's/>comp(\d+)(\S+)\s.+/comp$1$2\tc$1/' >Assembly_GoodCoralSymbiont_formapping_seq2iso.tab
[ysawall@turing1 Bowtie2_mapping]$ head Assembly_GoodCoralSymbiont_formapping_seq2iso.tab 
>TR309|c0_g1_i1_coral
>TR326|c0_g1_i1_coral
...
```
Table does **not** list what we need (it needs to be 2 columns with the second column listing the contig name without the isoform)

## =====08-11-2016 – Mapping (Mikhail Matz protocol)## =
Do bowtie2 mapping again, listing each sample sequence individually (input and output file)
```
[ysawall@turing1 Bowtie2_mapping]$ nano bt2mapping_all.sh

#! /bin/bash

#$ -cwd
#$ -o bt2mapping_all.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de

module load bowtie2/2.2.4

bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-3_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-6_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-7_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-7_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-8_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-8_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-DOG-9_R1_clippedtrimmedfilterd.fastq -S 2011-DOG-9_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-1_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-1_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-2_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-3_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-4_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-5_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-5_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-MAQ-6_R1_clippedtrimmedfilterd.fastq -S 2011-MAQ-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-2_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-3_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-4_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-7_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-7_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-8_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-8_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-WAJ-9_R1_clippedtrimmedfilterd.fastq -S 2011-WAJ-9_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-1_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-1_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-2_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-3_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-4_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-5_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-5_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2011-YAN-6_R1_clippedtrimmedfilterd.fastq -S 2011-YAN-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-1_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-1_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-2_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-3_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-4_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-6_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-DOG-7_R1_clippedtrimmedfilterd.fastq -S 2012-DOG-7_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-1_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-1_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-2_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-3_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-4_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-5_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-5_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-MAQ-6_R1_clippedtrimmedfilterd.fastq -S 2012-MAQ-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-4_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-5_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-5_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-6_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-7_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-7_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-8_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-8_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-WAJ-9_R1_clippedtrimmedfilterd.fastq -S 2012-WAJ-9_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-1_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-1_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-2_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-2_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-3_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-3_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-4_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-4_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-5_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-5_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5
bowtie2 --local -x Assembly_GoodCoralSymbiont_formapping -U 2012-YAN-6_R1_clippedtrimmedfilterd.fastq -S 2012-YAN-6_R1_clippedtrimmedfilterd_bt2.sam --no-unal -k 5

[ysawall@turing1 Bowtie2_mapping]$ qsub bt2mapping_2.sh
Your job 214943 ("bt2mapping_2.sh") has been submitted
```

Mapping was successful and created a sam file for each sample. 
In summary, the number of reads is mostly between 8 and 15 million of which 30-35% could not be aligned, 20-25 % were aligned once and 40-45 % were aligned > 1 time. In average about 67 % of reads could be aligned.

## =====09-11-2016 – isoform table ## =
Decided to do isoform table by hand in excel.
Take formally created seq2iso.tab file and change it to .txt file. Than copy isoform table to computer using scp. Not trivial! Finally figured it out...
```
[ysawall@turing1 Bowtie2_mapping]$ mv Assembly_GoodCoralSymbiont_formapping_seq2iso.tab Assembly_GoodCoralSymbiont_formapping_seq2iso.txt

#Then leave Terminal and start it again and do scp without logging in first

Yvonnes-MacBook-Pro:~ sawall$ scp ysawall@turing.hpc.odu.edu:/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/Assembly_GoodCoralSymbiont_formapping_seq2iso.txt ~/Desktop
ysawall@turing.hpc.odu.edu's password: 
Assembly_GoodCoralSymbiont_formapping_seq2iso 100% 4051KB   1.0MB/s   00:04   
```

In excel use "find and replace" to remove everything after the gene identifies (e.g. g1) by typing "_i*" into find and " " in replace. 
Replace vertical line by "_" (Find and replace function) and add _coral or _symbiont again. 

--> Problem: Although tab file was correctly displayed in TextEditor, it wasn't in Terminal. The tabs were replaced by the symbol "^" displaying the entire table as one line. This is Dan's explanation and solution:
I think it was an end of line character issue. Basically, there is an actual character signifying an "end of the line" (think a return) and it differs between operating systems (mac vs. windows). When you save a file as tab delimited text from excel, it saves the end of line characters as something different than that of a unix-linux platform. Any time you see all your lines of text appearing as a single line, this is likely the culprit. If you open a .txt file in the TextWrangler program (I highly advise you download this to your mac laptop and use it exclusively for text files), you can see what the end of line character is at the bottom of the screen (see attached screenshot). Your file was saved with "legacy mac (CR)" end of line characters. Unix systems recognize "LF" or "Line Feeds" vs "CR or Carriage Returns". Windows systems recognize both of them together (CRLF; confusing I know). Anyways, in TextWrangler you can easily select alternative end of line (EOL) characters and re-save the file in the new format. This is what I did and it is now uploaded to the cluster as "Assembly_GoodCoralSymbiont_formapping_seq2iso_final2_UNIXLF.txt". 

Downloaded TextWrangler.

## =====11-11-2016 – create count tables## =
Create count file with one sample, first, to see, if it works.

```
[ysawall@turing1 Bowtie2_mapping]$ head Assembly_GoodCoralSymbiont_formapping_seq2iso_final2_UNIXLF.txt
TR309|c0_g1_i1_coral	TR309_c0_g1_coral
TR326|c0_g1_i1_coral	TR326_c0_g1_coral
TR328|c0_g1_i1_coral	TR328_c0_g1_coral
TR470|c1_g1_i1_coral	TR470_c1_g1_coral
...
[ysawall@turing1 Bowtie2_mapping]$ /cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/scripts/tag-based_RNAseq/samcount.pl 2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam Assembly_GoodCoralSymbiont_formapping_seq2iso_final2_UNIXLF.txt aligner=bowtie2 > 2011-DOG-10_R1_clippedtrimmedfilterd_bt2_counts.txt
disregarding reads mapping to multiple isogroups

```
Connection to the cluster was disrupted at some point, therefore the script stopped. Tried again with submitting a qsub script.

```
[ysawall@turing1 Bowtie2_mapping]$ nano samcounts_test.sh
#! /bin/bash

#$ -cwd
#$ -o samcount_2011-DOG-10.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de

module load bowtie2/2.2.4

/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/scripts/tag-based_RNAseq/samcount.pl 2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam Assembly_GoodCoralSymbiont_formapping_seq2iso_final2_UNIXLF.txt aligner=bowtie2 > 2011-DOG-10_R1_clippedtrimmedfilterd_bt2_counts.txt

[ysawall@turing1 Bowtie2_mapping]$ qsub samcounts_test.sh 
Your job 216293 ("samcounts_test.sh") has been submitted
[ysawall@turing1 Bowtie2_mapping]$ qstat -u ysawall
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
 216293 500.00000 samcounts_ ysawall      r     11/11/2016 12:27:14 main@coreV2-22-007.cm.cluster      1        

# although it was running for a few hours, there was still now success. The count.txt file was empty. Check result file..

[ysawall@turing1 Bowtie2_mapping]$ head samcount_2011-DOG-10.txt
Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
Warning: Output file '2011-DOG-3_R1_clippedtrimmedfilterd.fastq' was specified without -S.  This will not work in future Bowtie 2 versions.  Please use -S instead.
Extra parameter(s) specified: "2011-DOG-6_R1_clippedtrimmedfilterd.fastq", "2011-DOG-7_R1_clippedtrimmedfilterd.fastq",...

```

Try again with -S in front of output file in the script, as indicated in the result file (samcount_2011-DOG-10.txt)

```
[ysawall@turing1 Bowtie2_mapping]$ nano samcounts_test.sh
#! /bin/bash

#$ -cwd
#$ -o samcount_2011-DOG-10.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de

module load bowtie2/2.2.4

/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/scripts/tag-based_RNAseq/samcount.pl 2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam Assembly_GoodCoralSymbiont_formapping_seq2iso_final2_UNIXLF.txt aligner=bowtie2 -S 2011-DOG-10_R1_clippedtrimmedfilterd_bt2_counts.txt

[ysawall@turing1 Bowtie2_mapping]$ qsub samcounts_test.sh 
Your job 216569 ("samcounts_test.sh") has been submitted
[ysawall@turing1 Bowtie2_mapping]$ qstat -u ysawall                             job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
 216569 500.00000 samcounts_ ysawall      r     11/11/2016 17:24:05 main@coreV3-23-017.cm.cluster      1        

```

again didn't work

```
[ysawall@turing1 Bowtie2_mapping]$ head samcount_2011-DOG-10.txt 
Warning: no access to tty (Bad file descriptor).
Thus no job control in this shell.
disregarding reads mapping to multiple isogroups
Killed
```

## =====Beginning of 2017 – make isoform table and count table again ## =
with Mikhail's help...
Found out that the isoform table is wrong, therefore I re-did the isoform table following Mikhail's suggestion
```
[ysawall@turing1 ~]$ cd /cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/
[ysawall@turing1 Bowtie2_mapping]$ grep ">" Assembly_GoodCoralSymbiont_formapping.fasta | perl -pe 's/>(TR(\d+)\S+).+/$1\tisogroup$2/' > Assembly_GoodCoralSymbiont_formapping_seq2iso.tab 
[ysawall@turing1 Bowtie2_mapping]$ head Assembly_GoodCoralSymbiont_formapping_seq2iso.tab
TR309|c0_g1_i1_cora isogroup309
TR326|c0_g1_i1_cora isogroup326
TR328|c0_g1_i1_cora isogroup328
TR470|c1_g1_i1_cora isogroup470
...
# --> Problem: the word "coral" is incomplete ("l" missing)
# Do it again with a slightly different command line

[ysawall@turing1 Bowtie2_mapping]$ grep ">" Assembly_GoodCoralSymbiont_formapping.fasta | perl -pe 's/>(TR(\d+)\S+)/$1\tisogroup$2/' >Assembly_GoodCoralSymbiont_formapping_seq2iso.tab
[ysawall@turing1 Bowtie2_mapping]$ head Assembly_GoodCoralSymbiont_formapping_seq2iso.tab
TR309|c0_g1_i1_coral	isogroup309
TR326|c0_g1_i1_coral	isogroup326
TR328|c0_g1_i1_coral	isogroup328
...
# --> worked!!

```
**Run samcount.pl**
I probably did it the complicated way by writing a sh script for each sample (sam file), but it seems to have worked following the following example for 2011-DOG-3...
```
[ysawall@turing1 Bowtie2_mapping]$ nano samcount-2011-DOG3.sh
#! /bin/bash

#$ -cwd
#$ -o samcount_result_2011-DOG-3.txt -j y
#$ -q main
#$ -m eas
#$ -M ysawall@geomar.de

module load bowtie2/2.2.4

/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/scripts/tag-based_RNAseq/samcount.pl 2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam Assembly_GoodCoralSymbiont_formapping_seq2iso.tab aligner=bowtie2 >2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam.counts

[ysawall@turing1 Bowtie2_mapping]$ qsub samcount-2011-DOG3.sh
...
[ysawall@turing1 Bowtie2_mapping]$ head 2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam.counts
isogroup100	108
isogroup100002	136
isogroup100003	44
isogroup100009	32
...

# move all sam.counts file in a new directory

[ysawall@turing1 Bowtie2_mapping]$ mkdir ./samcounts
[ysawall@turing1 Bowtie2_mapping]$ mv *bt2.sam.counts ./samcounts/
[ysawall@turing1 Bowtie2_mapping]$ ls ./samcounts/
2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam.counts
2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam.counts
2011-DOG-6_R1_clippedtrimmedfilterd_bt2.sam.counts
2011-DOG-7_R1_clippedtrimmedfilterd_bt2.sam.counts
2011-DOG-8_R1_clippedtrimmedfilterd_bt2.sam.counts
....

# combine sam.counts files

[ysawall@turing1 Bowtie2_mapping]$ cd ./samcounts/
[ysawall@turing1 samcounts]$ /cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/scripts/tag-based_RNAseq/expression_compiler.pl *sam.counts > allcounts.txt
[ysawall@turing1 samcounts]$ head allcounts.txt 
	2011-DOG-10_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-DOG-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-DOG-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-DOG-7_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-DOG-8_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-DOG-9_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-1_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-5_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-MAQ-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-7_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-8_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-WAJ-9_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-1_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-5_R1_clippedtrimmedfilterd_bt2.sam.counts	2011-YAN-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-1_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-DOG-7_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-1_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-5_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-MAQ-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-5_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-6_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-7_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-8_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-WAJ-9_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-1_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-2_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-3_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-4_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-5_R1_clippedtrimmedfilterd_bt2.sam.counts	2012-YAN-6_R1_clippedtrimmedfilterd_bt2.sam.counts	
isogroup100	52	108	226	91	31	75	28	97	56	34	121	62	98	57	68	42	60	38	51	82	77	83	50	46	0	0	1	0	71	82	0	60	40	152	88	2	19	187	49	200	60	42	21	52	19	6	
isogroup100002	131	136	665	109	72	114	54	139	73	95	129	125	152	149	185	121	158	110	179	278	127	110	159	142	2	5	1	0	130	147	3	64	84	78	168	15	44	227	101	188	115	128	99	240	89	51	
...

# --> success!!
```

copy allcount.txt to computer

```
# open new Terminal window and go to directory of where you want to copy the file to (I did it into the GEOMAR directory, because other folders (e.g. Jeddah Daten) had a gap between words, which doesn't work in Terminal

Yvonnes-MacBook-Pro:~ sawall$ ls
3166.sh				Movies
Desktop				Music
Documents			Pictures
Downloads			Public
Dropbox				ZipCloud.exe
Google Drive			install_flash_player_osx.dmg
Library				searchGenius.dmg
MacKeeper.3.5.1.pkg
Yvonnes-MacBook-Pro:~ sawall$ cd ./Documents/GEOMAR/
Yvonnes-MacBook-Pro:GEOMAR sawall$ scp ysawall@turing.hpc.odu.edu:/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping/samcounts/allcounts.txt .
ysawall@turing.hpc.odu.edu's password: 
allcounts.txt                                 100%   10MB 924.6KB/s   00:11    

# transfer totalannotated.txt file, as well

Yvonnes-MacBook-Pro:GEOMAR sawall$ scp ysawall@turing.hpc.odu.edu:/cm/shared/courses/dbarshis/RedSea/fastas/totalannotation/Assembly_GoodCoralSymbiont_totalannotated.txt .
ysawall@turing.hpc.odu.edu's password: 
Assembly_GoodCoralSymbiont_totalannotated.txt 100%   85MB 584.9KB/s   02:29  
```

**Need to add sequence names first and divide allcounts.txt into "coral" and "symbionts"**

Extract sequence names from the GoodCoralSymbiont fasta file (used for mapping)

```
[ysawall@turing1 Bowtie2_mapping]$ pwd
/cm/shared/courses/dbarshis/RedSea/Bowtie2_mapping
[ysawall@turing1 Bowtie2_mapping]$ grep '>' Assembly_GoodCoralSymbiont_formapping.fasta | cut -d '>' -f 2 > sequencenames.txt
[ysawall@turing1 Bowtie2_mapping]$ head sequencenames.txt 
TR309|c0_g1_i1_coral
TR326|c0_g1_i1_coral
TR328|c0_g1_i1_coral
...

# add "contig" as title for column in sequencenames.txt

[ysawall@turing1 Bowtie2_mapping]$ nano sequencenames.txt 
contig
TR309|c0_g1_i1_coral
TR326|c0_g1_i1_coral
TR328|c0_g1_i1_coral
...

```
!! --> doesn't work for the next step (add sequence names to sam.counts files), because the sam.counts files have different sequence names now (isoform...) !! see below

```
[ysawall@turing1 samcounts]$ head 2012-MAQ-6_R1_clippedtrimmedfilterd_bt2.sam.counts
isogroup100	152
isogroup100002	78
isogroup100003	39
isogroup100005	67
isogroup100007	127
```

--> Renaming in excel: sorting isoform names alphabetically (both tables), remove duplicates in naming table "Assembly_GoodCoralSymbiont_formapping_seq2iso.tab", check, if the order and total number of rows in both tables is the same (e.g. by using the IF function in the 3rd row: IF(A1=A2,1,0); then check min and max values in 3rd row, which should both be 1), add row with contig names to "allcounts.txt" and delete the row with the isoform names.

[[namespace:page#here|title]]
