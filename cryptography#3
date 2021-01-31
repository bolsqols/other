void init_ctr(struct ctr_state *state, const unsigned char iv[16])
{        
    state->num = 0;
    memset(state->ecount, 0, 16);
    memcpy(state->ivec, iv, 16);
}

void crypt_message(const u8* src, u8* dst, unsigned int src_len, const AES_KEY* key, const u8* iv)
{   
   struct ctr_state state;
   init_ctr(&state, iv);
   AES_ctr128_encrypt(src, dst, src_len, key, state.ivec, state.ecount, &state.num);
}

int main()
{
   int len;
   char source[128];
   char cipher[128];
   char recovered[128];
   unsigned char iv[AES_BLOCK_SIZE];

   const unsigned char* enc_key = (const unsigned char*)"qwerty1234567QqDRZ";

   if(!RAND_bytes(iv, AES_BLOCK_SIZE)) 
   {
       fprintf(stderr, "Could not create random bytes.");
       exit(1);    
   }

   AES_KEY key;
   AES_set_encrypt_key(enc_key, 128, &key);

   strcpy(source, "Dauren");
   len = strlen(source);
   memset(recovered, 0, sizeof(recovered));
   crypt_message((const u8*)source, (u8*)cipher, len, &key, iv);
   crypt_message((const u8*)cipher, (u8*)recovered, len, &key, iv);
   printf("Recovered text:%s\n", recovered);

   strcpy(source, "Nurkeldy");
   len = strlen(source);
   memset(recovered, 0, sizeof(recovered));
   crypt_message((const u8*)source, (u8*)cipher, len, &key, iv);
   crypt_message((const u8*)cipher, (u8*)recovered, len, &key, iv);
   printf("Recovered text:%s\n", recovered);

   return 0;
}
//encrypt decryp
/*void crypt_file(const u8* src_file, const u8* dst_file, const AES_KEY* key, const u8* iv)
{   
   struct ctr_state state;
   init_ctr(&state, iv);

   const int buffer_size = 512; 
   unsigned char buffer_in[buffer_size];
   unsigned char buffer_out[buffer_size];
   int bytes_read;

   //open files and/or socket
   //file/message loop
   {
      //read source, obtain buffer_in and bytes_read
      AES_ctr128_encrypt(buffer_in, buffer_out, bytes_read, key, state.ivec, state.ecount, &state.num);
      //write buffer_out/bytes_read to destination
   }
   //close handles
}*/
