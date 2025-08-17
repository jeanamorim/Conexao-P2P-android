# Conexão P2P Android - React Native

Esta solução permite conectar dois dispositivos Android diretamente via rede local para troca de dados de pagamento, sem necessidade de servidor externo.

## Arquitetura P2P

- **Dispositivo A**: Cliente de pagamento (busca e conecta ao Dispositivo B)
- **Dispositivo B**: Servidor de pagamento (inicia servidor TCP e processa pagamentos)
- **Comunicação Direta**: TCP Socket + Zeroconf para descoberta automática

## Tecnologias Utilizadas

- **React Native**: Framework mobile
- **TypeScript**: Tipagem estática
- **react-native-tcp-socket**: Comunicação TCP direta
- **react-native-zeroconf**: Descoberta automática de serviços na rede

## Como Usar

### 1. Instalar Dependências

\`\`\`bash
npm install
# ou
yarn install
\`\`\`

### 2. Configurar os Dispositivos

1. Instale o app React Native nos dois dispositivos Android
2. Certifique-se de que ambos estão na mesma rede Wi-Fi
3. No app, selecione o tipo de dispositivo (A ou B)

### 3. Iniciar a Conexão

1. **Dispositivo B**: 
   - Selecione "DISPOSITIVO B"
   - Clique em "Iniciar Servidor"
   - O dispositivo anunciará o serviço na rede

2. **Dispositivo A**:
   - Selecione "DISPOSITIVO A" 
   - Clique em "Buscar Dispositivos"
   - Selecione o Dispositivo B encontrado para conectar

### 4. Testar Pagamentos

1. **Dispositivo A**: Digite valor e descrição, clique em "Enviar Pagamento"
2. **Dispositivo B**: Processará automaticamente e retornará o resultado
3. **Dispositivo A**: Receberá confirmação de aprovação/rejeição

## Funcionalidades

### Dispositivo A (Cliente)
- ✅ Descoberta automática via Zeroconf
- ✅ Conexão TCP direta ao Dispositivo B
- ✅ Envio de dados de pagamento
- ✅ Recebimento de confirmações
- ✅ Interface intuitiva com logs em tempo real
- ✅ Histórico de transações

### Dispositivo B (Servidor)
- ✅ Servidor TCP na porta 8080
- ✅ Anúncio automático via Zeroconf
- ✅ Processamento de pagamentos (70% aprovação)
- ✅ Resposta automática ao cliente
- ✅ Logs detalhados de conexões
- ✅ Histórico de pagamentos processados

## Estrutura de Dados

### Pagamento Enviado (PaymentData)
\`\`\`typescript
{
  id: string
  amount: number
  description: string
  timestamp: number
}
\`\`\`

### Resposta do Pagamento (PaymentResponse)
\`\`\`typescript
{
  id: string
  success: boolean
  message: string
  timestamp: number
}
\`\`\`

## Arquivos Principais

- `src/screens/DeviceAScreen.tsx` - Interface do cliente
- `src/screens/DeviceBScreen.tsx` - Interface do servidor
- `src/types/index.ts` - Definições TypeScript
- `App.tsx` - Seletor de dispositivo

## Troubleshooting

1. **Dispositivos não se conectam**: 
   - Verifique se estão na mesma rede Wi-Fi
   - Reinicie o servidor no Dispositivo B

2. **Serviço não encontrado**:
   - Aguarde alguns segundos após iniciar o servidor
   - Tente buscar novamente no Dispositivo A

3. **Conexão instável**:
   - Verifique a qualidade da rede Wi-Fi
   - Mantenha os dispositivos próximos ao roteador

4. **Pagamentos não processam**:
   - Verifique os logs para erros de conexão
   - Reconecte os dispositivos se necessário

## Permissões Android

Adicione as seguintes permissões no `android/app/src/main/AndroidManifest.xml`:

<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_MULTICAST_STATE" />

## Próximos Passos

- [ ] Adicionar criptografia nas comunicações
- [ ] Implementar autenticação entre dispositivos
- [ ] Adicionar reconexão automática
- [ ] Melhorar tratamento de erros de rede
- [ ] Adicionar suporte a múltiplos clientes
- [ ] Implementar persistência local de dados
