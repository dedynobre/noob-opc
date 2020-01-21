# Configurações

Configurações de testes de um OPC Server usando node red.
```javascript
function constructAlarmAddressSpace(server, addressSpace, eventObjects, done) {

    const LocalizedText = coreServer.core.nodeOPCUA.LocalizedText
    const namespace = addressSpace.getOwnNamespace()

    coreServer.internalDebugLog('init dynamic address space')
    node.warn('Montando a arvore de variaveis OPC')
	
	const rootFolder = addressSpace.findNode("RootFolder");
	
	// ---------------------------------------------------------------------
	// adicionar pastas no projeto
	// ---------------------------------------------------------------------
	
	let dados = namespace.addFolder(rootFolder.objects, { "browseName": "Dados" });
		
	// ---------------------------------------------------------------------
	
	// ---------------------------------------------------------------------
	// adicionar sub pastas no projeto
	// ---------------------------------------------------------------------
	
	let pEntradas = namespace.addFolder(dados, { "browseName": "Entradas" });
	let pSaidas = namespace.addFolder(dados, { "browseName": "Saidas" });
		
	// ---------------------------------------------------------------------	
	
    // ---------------------------------------------------------------------
	// variaveis leitura/escrita
	// no primeiro instante que o servidor é iniciado escreve o valor de 0.1
	// ---------------------------------------------------------------------
	
    if(scriptObjects.var01 === undefined || scriptObjects.var01 === null) {
            scriptObjects.var01 = 0.1
    }
	
    if(scriptObjects.var03 === undefined || scriptObjects.var03 === null) {
            scriptObjects.var03 = 0.1
    }
	
	// ---------------------------------------------------------------------
    	
	// ---------------------------------------------------------------------
	// variaveis fixas
	// ---------------------------------------------------------------------
	
    let var02 = 25.0
	
	// ---------------------------------------------------------------------
	
	// ---------------------------------------------------------------------
	// variaveis para cada pasta
	// ---------------------------------------------------------------------
	
	// ---------------------------------------------------------------------
	
    namespace.addVariable({
        //nodeId: 'ns=1;i=var_01',
        browseName: 'Variavel 01',
		organizedBy: pEntradas,
        dataType: 'Double',
        value: {
            get: function () {
                return new coreServer.core.nodeOPCUA.Variant({
                    dataType: 'Double',
                    value: scriptObjects.var01
                })
            },
            set: function (variant) {
                scriptObjects.var01 = parseFloat(variant.value)
                return coreServer.core.nodeOPCUA.StatusCodes.Good
            }
        }
        
    })
	
	// ---------------------------------------------------------------------
	
    namespace.addVariable({
        //nodeId: 'ns=1;i=var_02',
        browseName: 'Variavel 02',
		organizedBy: pEntradas,
        dataType: 'Double',
        value: {
            get: function () {
                return new coreServer.core.nodeOPCUA.Variant({
                  dataType: 'Double',
                  value: var02
                })
            }
        }
        
    })
	
	// ---------------------------------------------------------------------
	
    namespace.addVariable({
        //nodeId: 'ns=1;i=var_01',
        browseName: 'Variavel 03',
		organizedBy: pEntradas,
        dataType: 'Double',
        value: {
            get: function () {
                return new coreServer.core.nodeOPCUA.Variant({
                    dataType: 'Double',
                    value: scriptObjects.var03
                })
            },
            set: function (variant) {
                scriptObjects.var03 = parseFloat(variant.value)
                return coreServer.core.nodeOPCUA.StatusCodes.Good
            }
        }
        
    })
	
	// ---------------------------------------------------------------------
    
    done()
}

```
 
