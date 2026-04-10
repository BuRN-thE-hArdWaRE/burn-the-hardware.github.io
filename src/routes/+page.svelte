<script>
  import { Canvas } from '@threlte/core';
  import Scene from '../lib/scene.svelte';
  import '../lib/styles/app.css';

  let isEnabled = $state(false);
  let theme = $state('default');

  function handleClick() {
    isEnabled = true;
  }

  const themes = [
    { id: 'default', label: 'Dark' },
    { id: 'dark', label: 'Midnight' }
  ];
</script>

<div class="theme-{theme} min-h-screen transition-colors duration-500">
  <div class="fixed top-6 right-6 z-50 flex items-center gap-1 p-1 bg-slate-900/50 backdrop-blur-xl border border-white/10 rounded-full shadow-2xl">
    {#each themes as t}
      <button 
        onclick={() => theme = t.id}
        class="px-4 py-1.5 rounded-full text-[10px] font-bold uppercase tracking-widest transition-all
        {theme === t.id ? 'bg-orange-500 text-white shadow-lg shadow-orange-500/20' : 'text-slate-400 hover:text-white'}"
      >
        {t.label}
      </button>
    {/each}
  </div>

  <main class="bg-theme-bg selection:bg-orange-500/30 text-theme-text transition-colors duration-500">
    <section class="relative flex h-dvh w-full items-center justify-center overflow-hidden bg-theme-bg px-4">
        <div class="absolute inset-0 z-0 opacity-[0.15]" 
             style="background-image: linear-gradient(var(--grid-color) 1px, transparent 1px), linear-gradient(90deg, var(--grid-color) 1px, transparent 1px); background-size: 30px 30px;">
        </div>
        
        <div class="relative z-10 text-center w-full flex flex-col items-center">
            <div class="mb-6 inline-flex items-center gap-2 px-3 py-1.5 border border-orange-500/20 bg-orange-500/5 text-orange-500 text-[10px] font-tech uppercase tracking-[0.2em] rounded-sm">
                <span class="relative flex h-2 w-2">
                    <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-orange-400 opacity-75"></span>
                    <span class="relative inline-flex rounded-full h-2 w-2 bg-orange-500"></span>
                </span>
                Hardware System v1.0
            </div>

            <h1 class="w-full text-[clamp(2.5rem,11.5vw,8rem)] font-bold tracking-tighter text-theme-heading uppercase italic leading-none whitespace-nowrap">
                AE<span class="text-orange-500 not-italic">_</span>CS
            </h1>

            <p class="mt-6 text-slate-500 font-tech text-[10px] sm:text-xs uppercase tracking-[0.2em] max-w-70 sm:max-w-md mx-auto leading-relaxed">
                Adaptive Edge<br class="sm:hidden"/> - Control System
            </p>
        </div>
    </section>

    <section class="py-20 bg-theme-bg border-t border-theme-border">
                <div class="max-w-6xl mx-auto px-6">
                    
                </div>
    </section>

    <section class="py-20 bg-theme-bg border-t border-theme-border">
        <div class="max-w-6xl mx-auto px-6">
            <div class="mb-12">
                <span class="text-orange-500 font-tech font-bold text-[10px] uppercase tracking-[0.2em]">Visualizer</span>
                <h3 class="text-3xl font-bold text-theme-heading uppercase mt-2">Digital Twin <span class="text-slate-500">v1.0</span></h3>
            </div>
            
            <div class="h-125 w-full rounded-lg border border-theme-border bg-theme-bg-alt overflow-hidden relative group">
                <div class="relative w-full h-125 flex items-center justify-center">
                    {#if !isEnabled}
                        <button 
                            type="button" 
                            onclick={handleClick}
                            class="z-10 px-10 py-5 bg-white/10 hover:bg-white/20 text-theme-heading border border-white/20 rounded-full backdrop-blur-md transition-all active:scale-95 font-medium tracking-wide"
                        >
                        Load 3D Model
                        </button>
                    {/if}

                    {#if isEnabled}
                        <Canvas rendererParameters={{ alpha: true }}>
                            <Scene />
                        </Canvas>
                    {/if}
                </div>
                <div class="absolute bottom-3 right-3 flex items-center gap-2 px-3 py-1.5 rounded-full bg-slate-900/80 border border-slate-700 backdrop-blur-sm opacity-80 hover:opacity-100 transition-opacity">
                    <a href="https://github.com/threlte/threlte/blob/main/LICENSE.md" target="_blank" rel="noopener noreferrer" class="flex items-center gap-2 text-xs text-slate-300 hover:text-white transition-colors">
                        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"/><path d="M9 18c-4.51 2-5-2-7-2"/></svg>
                        <span class="font-medium border-l border-slate-700 pl-2">MIT License</span>
                    </a>
                </div>
            </div>
        </div>
    </section>

<section id="about" class="py-20 md:py-32 px-4 md:px-6 bg-theme-bg">
    <div class="max-w-4xl mx-auto">
        <div class="flex items-center gap-4 mb-8 md:mb-12">
            <h3 class="text-xl md:text-2xl font-bold tracking-tight text-white-heading uppercase whitespace-nowrap">Hackathon Specs</h3>
            <div class="h-px grow bg-slate-800"></div>
        </div>
        
        <div class="overflow-hidden rounded-xl border border-theme-border bg-theme-bg-alt shadow-2xl">
            <table class="w-full text-left border-collapse">
                <thead>
                    <tr class="border-b border-slate-800 bg-slate-900/50 text-slate-500 font-mono text-[10px] uppercase tracking-[0.2em]">
                        <th class="p-4 md:p-6 font-semibold">Component Registry</th>
                        <th class="p-4 md:p-6 text-right font-semibold">Total</th>
                    </tr>
                </thead>
                <tbody class="divide-y divide-slate-800/40">
                    <tr class="group transition-colors duration-300 hover:bg-orange-500/3">
                        <td class="p-4 md:p-6">
                            <span class="block font-bold text-base md:text-lg text-slate-100 group-hover:text-orange-400">GLYPH S3</span>
                            <span class="text-[10px] md:text-xs font-mono text-slate-500 uppercase tracking-tight">Main Controller</span>
                        </td>
                        <td class="p-4 md:p-6 text-right font-mono font-bold text-lg md:text-xl text-slate-300 group-hover:text-orange-400">₹799</td>
                    </tr>

                    <tr class="group transition-colors duration-300 hover:bg-orange-500/3">
                        <td colspan="2" class="p-0">
                            <details class="group/details">
                                <summary class="flex items-center justify-between p-4 md:p-6 cursor-pointer list-none outline-none">
                                    <div>
                                        <div class="flex items-center gap-2">
                                            <span class="block font-bold text-base md:text-lg text-slate-100 group-hover:text-orange-400">Drive Train</span>
                                            <svg class="w-4 h-4 text-slate-500 group-open/details:rotate-180 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                            </svg>
                                        </div>
                                        <span class="text-[10px] md:text-xs font-mono text-slate-500 uppercase tracking-tight">Motors & Motion Control</span>
                                    </div>
                                    <div class="text-right font-mono font-bold text-lg md:text-xl text-slate-300 group-hover:text-orange-400">₹459</div>
                                </summary>
                                <div class="px-4 pb-6 md:px-10 md:pb-8">
                                    <div class="space-y-3 border-l-2 border-slate-800 pl-4 md:pl-6">
                                        <div class="flex justify-between items-center">
                                            <span class="text-sm font-semibold text-slate-300 uppercase">BO Motors <span class="text-[10px] text-slate-500 ml-1">x2</span></span>
                                            <span class="font-mono text-sm text-slate-400">₹200</span>
                                        </div>
                                        <div class="flex justify-between items-center">
                                            <span class="text-sm font-semibold text-slate-300 uppercase">Motor Wheels <span class="text-[10px] text-slate-500 ml-1">x2</span></span>
                                            <span class="font-mono text-sm text-slate-400">₹60</span>
                                        </div>
                                        <div class="flex justify-between items-center">
                                            <span class="text-sm font-semibold text-slate-300 uppercase">Motor Driver [TB6612FNG]</span>
                                            <span class="font-mono text-sm text-slate-400">₹199</span>
                                        </div>
                                    </div>
                                </div>
                            </details>
                        </td>
                    </tr>

                    <tr class="group transition-colors duration-300 hover:bg-orange-500/3">
                        <td colspan="2" class="p-0">
                            <details class="group/details">
                                <summary class="flex items-center justify-between p-4 md:p-6 cursor-pointer list-none outline-none">
                                    <div>
                                        <div class="flex items-center gap-2">
                                            <span class="block font-bold text-base md:text-lg text-slate-100 group-hover:text-orange-400">Power Source</span>
                                            <svg class="w-4 h-4 text-slate-500 group-open/details:rotate-180 transition-transform" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                            </svg>
                                        </div>
                                        <span class="text-[10px] md:text-xs font-mono text-slate-500 uppercase tracking-tight">Voltage Regulation & Cells</span>
                                    </div>
                                    <div class="text-right font-mono font-bold text-lg md:text-xl text-slate-300 group-hover:text-orange-400">₹699</div>
                                </summary>
                                <div class="px-4 pb-6 md:px-10 md:pb-8">
                                    <div class="space-y-3 border-l-2 border-slate-800 pl-4 md:pl-6">
                                        <div class="flex justify-between items-center">
                                            <span class="text-sm font-semibold text-slate-300 uppercase">Li-Po Battery <span class="text-[10px] text-slate-500 ml-1">x2</span></span>
                                            <span class="font-mono text-sm text-slate-400">₹600</span>
                                        </div>
                                        <div class="flex justify-between items-center">
                                            <span class="text-sm font-semibold text-slate-300 uppercase">Buck Converter</span>
                                            <span class="font-mono text-sm text-slate-400">₹99</span>
                                        </div>
                                    </div>
                                </div>
                            </details>
                        </td>
                    </tr>

                    <tr class="group transition-colors duration-300 hover:bg-orange-500/3">
                        <td class="p-4 md:p-6">
                            <span class="block font-bold text-base md:text-lg text-slate-100 group-hover:text-orange-400">I2C Display (1.3'')</span>
                            <span class="text-[10px] md:text-xs font-mono text-slate-500 uppercase tracking-tight">Main Controller</span>
                        </td>
                        <td class="p-4 md:p-6 text-right font-mono font-bold text-lg md:text-xl text-slate-300 group-hover:text-orange-400">₹200</td>
                    </tr>

                </tbody>

                <tfoot class="bg-slate-900/80 border-t-2 border-orange-500/50">
                    <tr>
                        <td class="p-4 md:p-6 font-bold text-[10px] md:text-xs uppercase text-slate-400 tracking-widest">Total Expenses</td>
                        <td class="p-4 md:p-6 text-right font-mono font-black text-xl md:text-2xl text-slate-100">₹2,157</td>
                    </tr>
                    <tr class="bg-orange-500/10">
                        <td class="p-4 md:p-6 font-bold text-[10px] md:text-xs uppercase text-orange-500/80 tracking-widest">Remaining <span class="text-slate-400">(of ₹4,000)</span></td>
                        <td class="p-4 md:p-6 text-right font-mono font-black text-2xl md:text-3xl text-orange-500">₹1,843</td>
                    </tr>
                </tfoot>
            </table>
        </div>
    </div>
</section>
<section id="hardware-spec" class="py-32 bg-theme-bg px-6 border-t border-theme-border">
    <div class="max-w-6xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-2 gap-16 items-start mb-20">
            <div>
                <h3 class="text-4xl md:text-5xl font-bold tracking-tighter mb-6 uppercase text-theme-heading leading-none">Hardware<br/><span class="text-orange-500">Architecture</span></h3>
                <p class="text-slate-400 leading-relaxed font-light max-w-md border-l-2 border-orange-500/30 pl-6">
                    System mapping optimized for ESP32 C3. Low-latency I2C wiring ensures 400kHz telemetry frequency for the MPU6050 sensor array.
                </p>
            </div>
            <div class="grid grid-cols-1 gap-3">
                        <div class="flex items-center justify-between p-4 rounded-md border border-slate-800 bg-slate-900/20 font-tech hover:border-orange-500/50 transition-all">
                            <span class="text-slate-500 text-[10px] uppercase tracking-widest">Master_SDA</span>
                            <span class="font-bold text-orange-500 text-lg">GPIO 21</span>
                        </div>
                        <div class="flex items-center justify-between p-4 rounded-md border border-slate-800 bg-slate-900/20 font-tech hover:border-orange-500/50 transition-all">
                            <span class="text-slate-500 text-[10px] uppercase tracking-widest">Master_SCL</span>
                            <span class="font-bold text-orange-500 text-lg">GPIO 22</span>
                        </div>
                        <div class="flex items-center justify-between p-4 rounded-md border border-slate-800 bg-slate-900/20 font-tech hover:border-orange-500/50 transition-all">
                            <span class="text-slate-500 text-[10px] uppercase tracking-widest">PWM_Output_Array</span>
                            <span class="font-bold text-slate-300 text-lg">13, 12, 14, 27</span>
                        </div>
                    </div>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
                <div class="group p-8 border border-slate-800 hover:border-orange-500/50 transition-all bg-slate-900/20 rounded-sm relative">
                    <div class="absolute top-0 right-0 p-2 opacity-20 group-hover:opacity-100 transition-opacity">
                        <div class="w-2 h-2 bg-orange-500 rounded-full"></div>
                    </div>
                    <span class="text-orange-500 font-tech font-bold text-[10px] uppercase tracking-[0.2em]">Telemetry</span>
                    <h4 class="text-xl font-bold mt-2 uppercase text-white tracking-tight">MPU6050 Node</h4>
                    <div class="h-px w-8 bg-slate-700 my-6 group-hover:w-full transition-all duration-700"></div>
                    <p class="text-slate-500 text-sm font-tech leading-loose">
                        Address: <span class="text-slate-300">0x68</span><br/>
                        Bus Speed: <span class="text-slate-300">400kHz</span>
                    </p>
                </div>

                <div class="group p-8 border border-slate-800 hover:border-orange-500/50 transition-all bg-slate-900/20 rounded-sm relative">
                    <span class="text-orange-500 font-tech font-bold text-[10px] uppercase tracking-[0.2em]">Actuation</span>
                    <h4 class="text-xl font-bold mt-2 uppercase text-white tracking-tight">Servo Matrix</h4>
                    <div class="h-px w-8 bg-slate-700 my-6 group-hover:w-full transition-all duration-700"></div>
                    <p class="text-slate-500 text-sm font-tech leading-loose">
                        Freq: <span class="text-slate-300">50Hz</span><br/>
                        Resolution: <span class="text-slate-300">16-bit</span>
                    </p>
                </div>

                <div class="group p-8 border border-slate-800 hover:border-orange-500/50 transition-all bg-slate-900/20 rounded-sm relative">
                    <span class="text-orange-500 font-tech font-bold text-[10px] uppercase tracking-[0.2em]">Regulation</span>
                    <h4 class="text-xl font-bold mt-2 uppercase text-white tracking-tight">Power Rail</h4>
                    <div class="h-px w-8 bg-slate-700 my-6 group-hover:w-full transition-all duration-700"></div>
                    <p class="text-slate-500 text-sm font-tech leading-loose">
                        Input: <span class="text-slate-300">7.4V LiPo</span><br/>
                        Output: <span class="text-slate-300">5.0V / 3A</span>
                    </p>
                </div>
            </div>
        </div>
    </section>
  </main>

  <footer class="bg-theme-bg py-12 px-6 border-t border-theme-border transition-colors duration-500">
      <div class="max-w-6xl mx-auto flex flex-col md:flex-row justify-between items-center gap-8">
          <p class="font-tech text-[10px] text-orange-500 tracking-[0.3em]">
              <span class="text-theme-text">&copy; {new Date().getFullYear()}</span>
              <span class="font-bold ml-1">BuRN thE hArdWaRE</span>
          </p>
      </div>
  </footer>
</div>