Howden et al. TOMATO NUCLEAR PROTEOMICS
The two Galaxy pipelines can downloaded from https://github.com/remco-stam/nucprot/ 


## Pt 1. Data preprocessing

1. List with protein IDs manually extracted from Proteomics output file "proteinGroups.txt"
	- Shortened ID created by taking only gene number, not description
	e.g. from long IDs in column replace "\s" for "\t" and select first part, remove rest  
	- All Phyca11, "CON" and "REV" sequences were removed
	- Saved as Step1_proteomics_List.text

2. Edit supplied fasta file
	- Galaxy pipeline pt1 steps 1 to 4 show how the fasta file was: 
	transformed to table, descriptions removed, turned back into fasta
	- File saved as Step2_Tom_Pc.fasta
	- first entry was wrong, manually altered after downloading
	
3. Create fasta file with all sequences from proteomics data
	- Run create_subset.py
	specify List and Fasta file
	- Step3_Proteomics.fasta created, 3653 sequences
	
	
## Pt 2. Identification of nuclear proteins	
	
4. Upload Step3_Proteomics.fasta and look for nuclear proteins, galaxy pipline pt2
	- Run on Galaxy: 
	Wolf PSort (plant), NLStradamus, Predict NLS and NoD ran to detect nuclear localisations
	- Concatenate lists, remove duplicate lines using count
	- Saved as 140716_Nucl-IDs.txt 2548 genes
	
5. Create Venn diagram, using Venny
	- Sequence IDs are copied from lists in Galaxy pipeline and entered in Venny software
	  Oliveros (2007)
	

## Pt 3. Data Filtering
	    
6. Detect Proteins that are Present/Absent between treatments
	- Use R script: Detect_PresenceAbsence.R
	requires Step6_proteinLFQs2.txt 
	- Creates 8 files proteins UP/DOWN by presence absence at 8 and 24 hour (e.g. between infected / non infected) or within a treatment (e.g. up or down in non infected from 8 to 24 hour)
	- Create Venn Diagram using protein names for each list.
										