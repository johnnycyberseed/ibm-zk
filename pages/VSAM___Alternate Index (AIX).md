- a [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] [[VSAM/Cluster]]
	- contains a  [[VSAM/Component/Index]] and [[VSAM/Component/Data]]
	- allowing
		- logical records of a [[Data Set/Type/VSAM/Key-Sequenced (KSDS)]] or [[Data Set/Type/VSAM/Entry-Sequenced (ESDS)]] [[VSAM/Cluster]]
	- to be accessed sequentially by more than one key field.
- Can use the [[utility/IDCAMS]] to define and create an AIX.
	- by including the ((6877de3f-7502-4fe4-b15d-2373eaf086f6)) command
- Before you can access such data sets via their alternate indexes, a path must be defined in the catalog
	- this is done through the [[utility/IDCAMS]]'s ((6877df4d-343a-4b81-b943-3600c5e8183f)) command