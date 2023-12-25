<script>
    import { onMount } from 'svelte';
    import { createClient } from '@supabase/supabase-js';
  
    const supabaseUrl = 'https://kjznqmhhzhkwuwzkagfw.supabase.co';
    const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Imtqem5xbWhoemhrd3V3emthZ2Z3Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDI5ODI5ODgsImV4cCI6MjAxODU1ODk4OH0.FG7EYEO91ueST6gZq3Mkp644jQ9s_Ubp52LGBmTNqZk';
    const supabase = createClient(supabaseUrl, supabaseKey);
  
    let data = [];
    let inputValue = '';
  
    const fetchData = async () => {
      const { data: records, error } = await supabase.from('Tabela01').select('*');
      if (error) {
        console.error('Erro ao buscar dados:', error);
      } else {
        data = records;
      }
    };
  
    const addData = async () => {
      if (inputValue.trim() !== '') {
        const { data: newRecord, error } = await supabase.from('Tabela01').insert([{ 'Coluna01': inputValue }]).select();
        if (error) {
          console.error('Erro ao adicionar dados:', error);
        } else {
            console.log(newRecord);
          data = [...data, newRecord[0]];
          inputValue = '';
        }
      }
    };
  
    onMount(() => {
      fetchData();
    });
  </script>
  
  <h1>Supabase App</h1>
  
  <form on:submit|preventDefault={addData}>
    <input type="text" bind:value={inputValue} placeholder="Digite um valor" />
    <button type="submit">Adicionar</button>
  </form>
  
  <ul>
    {#each data as item}
      <li>{item.Coluna01}</li>
    {/each}
  </ul>

<p>Alterado no github e no vscode</p>
<p>Alterado após publicado no Vercel</p>
  
