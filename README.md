<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Briefing Operativo v4.3 - Edición Premium</title>
    <script src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #0a0a0a; color: #f8fafc; -webkit-font-smoothing: antialiased; }
        .gold-text { color: #c5a059; }
        .gold-bg { background-color: #c5a059; }
        .gold-border { border-color: #c5a059; }
        .card-dark { background-color: #141414; border: 1px solid rgba(197, 160, 89, 0.1); }
        .animate-spin-custom { animation: spin 1.2s linear infinite; }
        @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
        .tap-highlight-transparent { -webkit-tap-highlight-color: transparent; }
        .btn-hover:active { transform: scale(0.96); transition: 0.1s; }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        const Icon = ({ name, size = 18, className = "" }) => {
            const icons = {
                calendar: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><rect width="18" height="18" x="3" y="4" rx="2" ry="2"/><line x1="16" x2="16" y1="2" y2="6"/><line x1="8" x2="8" y1="2" y2="6"/><line x1="3" x2="21" y1="10" y2="10"/></svg>,
                zap: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><polygon points="13 2 3 14 12 14 11 22 21 10 12 10 13 2"/></svg>,
                rotate: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M21 12a9 9 0 1 1-9-9c2.52 0 4.93 1 6.74 2.74L21 8"/><path d="M21 3v5h-5"/></svg>,
                alert: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><circle cx="12" cy="12" r="10"/><line x1="12" x2="12" y1="8" y2="12"/><line x1="12" x2="12.01" y1="16" y2="16"/></svg>,
                shield: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M12 22s8-4 8-10V5l-8-3-8 3v7c0 6 8 10 8 10z"/></svg>,
                userPlus: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/><circle cx="9" cy="7" r="4"/><line x1="19" x2="19" y1="8" y2="14"/><line x1="22" x2="16" y1="11" y2="11"/></svg>,
                coffee: <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round" className={className}><path d="M17 8h1a4 4 0 1 1 0 8h-1"/><path d="M3 8h14v9a4 4 0 0 1-4 4H7a4 4 0 0 1-4-4Z"/><line x1="6" x2="6" y1="2" y2="4"/><line x1="10" x2="10" y1="2" y2="4"/><line x1="14" x2="14" y1="2" y2="4"/></svg>
            };
            return icons[name] || null;
        };

        const App = () => {
            const [activeTab, setActiveTab] = useState('weekly');
            const [isSpinning, setIsSpinning] = useState(false);
            const [selectedResult, setSelectedResult] = useState(null);

            const staff = [
                // Mozos
                { name: "CHAVEZ ROGELIO", pos: "MOZO - LA IDEAL" },
                { name: "DUARTE WALTER ISAAC", pos: "MOZO - LA IDEAL" },
                { name: "HEREDIA LUDMILA", pos: "MOZO - LA IDEAL" },
                { name: "ORELLANA LUIS ROBERTO", pos: "MOZO - LA IDEAL" },
                { name: "RIVERO DESIREÉ AYELEN", pos: "MOZO - LA IDEAL" },
                { name: "ROBLES BALDOMERO", pos: "MOZO - LA IDEAL" },
                { name: "SANGUEZO LEONARDO SEBASTIÁN", pos: "MOZO - LA IDEAL" },
                { name: "YBARRA SOFIA", pos: "MOZA - LA IDEAL" },
                { name: "PEREZ EDGARDO NICOLAS", pos: "MOZO - LA IDEAL" },
                { name: "BOULLON JOSÉ ERNESTO", pos: "MOZO - LA IDEAL" },
                { name: "GARCIA EVELYN CELESTE", pos: "MOZA - LA IDEAL" },
                { name: "MONTENEGRO ENZO ARIEL", pos: "MOZO - LA IDEAL" },
                { name: "DE VINCENZO TOMÁS SEBASTIÁN", pos: "MOZO - LA IDEAL" },
                { name: "MARTINEZ NUÑEZ MAXIMO JUAN CRUZ", pos: "MOZO - LA IDEAL" },
                { name: "LLANOS DANIEL FABIAN", pos: "MOZO - LA IDEAL" },
                // Comis
                { name: "AYUNTA FABIANA", pos: "COMIS - LA IDEAL" },
                { name: "MEDINA TOBIAS", pos: "COMIS - LA IDEAL" },
                { name: "DELZOTTO LACROZ IARA AILEN", pos: "COMIS - LA IDEAL" },
                { name: "AGUIRRE NICOLAS LUCAS", pos: "COMIS - LA IDEAL" },
                { name: "DIAS KELLEN", pos: "COMIS - LA IDEAL" },
                { name: "SANCHEZ AYLEN JACQUELINE", pos: "COMIS - LA IDEAL" },
                { name: "ESCOBAR RICARDO", pos: "COMIS - LA IDEAL" },
                { name: "AQUINO FRANCO", pos: "COMIS - LA IDEAL" },
                // Recepcion
                { name: "FERNANDEZ LANZILLOTA AYELEN", pos: "RECEPCIÓN - LA IDEAL" },
                { name: "LAVAGNE ABRIL", pos: "RECEPCIÓN - LA IDEAL" },
                { name: "BARRIOS VENIALGO MARIA VIRGINIA", pos: "RECEPCIÓN - LA IDEAL" },
                { name: "MENDOZA LUCIA BELEN", pos: "RECEPCIÓN - LA IDEAL" },
                { name: "FRÍAS NATTALY GISEL", pos: "RECEPCIÓN - LA IDEAL" }
            ];

            const questionsPool = [
                // Operativas Generales
                "¿Cuál es el procedimiento cuando un cliente se olvida sus pertenencias?",
                "¿Cuáles son los 86 del día?",
                "¿Qué hacer si un cliente dice que su café está frío?",
                "¿Qué pasa si pido propina al cliente?",
                "¿Cuál es la venta sugestiva de hoy?",
                "¿Cuándo se hace el chequeo del segundo bocado?",
                "El cliente terminó de comer, ¿qué paso sigue?",
                "El cliente pide el cierre de la mesa, ¿qué paso hay que hacer a continuación?",
                "Si un cliente levanta la mano y no es de mi plaza, ¿qué hago?",
                "Como mozo, cuando termina mi turno y me retiro, ¿qué hago con mis mesas abiertas?",
                "Tengo la mesa sucia y un cliente espera por sentarse, ¿qué hago?",
                "¿Si tengo un faltante y el cliente pregunta por ese ítem, qué hago?",
                "¿Al bajar el Gran Té, qué tengo que decirle al cliente?",
                "VF: Al bajar las bebidas, las dejo en la mesa y me retiro.",
                "VF: Al fajinar lo hago de espaldas al salón.",
                "VF: El café está abierto pero el cliente está esperando hace mucho, lo bajo igual.",
                // Cafetería, Vinos y Coctelería
                "¿Qué variedad de café ofrece la confitería?",
                "¿Cuál es el maridaje correcto con un Rutini Rose respecto a nuestra carta?",
                "¿Cuál es la receta correcta de un Manhattan?",
                "¿Nuestra barra ofrece coctelería sin alcohol (Mocktails)?",
                "¿Cuáles son los ingredientes de un Negroni clásico?",
                "¿Qué variedades de vino ofrecemos en carta? (Nombra cepas o bodegas)",
                "¿Qué tipos de Té tenemos? Describe al menos UNO.",
                "Si un cliente pide un Macchiato, ¿qué debería recibir?",
                "¿Cuál es la diferencia principal entre un Latte y un Cappuccino?",
                "¿Qué es un Ristretto?",
                "¿Para qué sirve el sodín que acompaña al café?"
            ];

            const handleSpin = () => {
                setIsSpinning(true);
                setSelectedResult(null);
                setTimeout(() => {
                    const person = staff[Math.floor(Math.random() * staff.length)];
                    const question = questionsPool[Math.floor(Math.random() * questionsPool.length)];
                    setSelectedResult({ person, question });
                    setIsSpinning(false);
                }, 1000);
            };

            const handleNextPerson = () => {
                if (!selectedResult) return;
                const newPerson = staff[Math.floor(Math.random() * staff.length)];
                setSelectedResult(prev => ({ ...prev, person: newPerson }));
            };

            return (
                <div className="min-h-screen px-4 py-8 tap-highlight-transparent">
                    <div className="max-w-4xl mx-auto">
                        <header className="mb-10 border-l-[6px] gold-border pl-8 py-2">
                            <h1 className="text-4xl md:text-5xl font-light tracking-[0.25em] gold-text uppercase">LA IDEAL</h1>
                            <div className="flex items-center gap-4 mt-2">
                                <span className="text-white font-bold text-[10px] tracking-widest uppercase opacity-60 italic">Briefing Operativo v4.3</span>
                                <div className="h-[1px] bg-white/10 flex-1"></div>
                            </div>
                        </header>

                        <div className="grid grid-cols-1 lg:grid-cols-4 gap-8">
                            <nav className="space-y-3">
                                <button onClick={() => setActiveTab('weekly')} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition-all duration-300 btn-hover ${activeTab === 'weekly' ? 'gold-bg text-black font-bold shadow-2xl scale-[1.02]' : 'card-dark text-slate-400 hover:bg-[#222]'}`}>
                                    <Icon name="calendar" size={18}/> <span className="text-[10px] uppercase tracking-[0.2em]">Fijos</span>
                                </button>
                                <button onClick={() => setActiveTab('daily')} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition-all duration-300 btn-hover ${activeTab === 'daily' ? 'gold-bg text-black font-bold shadow-2xl scale-[1.02]' : 'card-dark text-slate-400 hover:bg-[#222]'}`}>
                                    <Icon name="zap" size={18}/> <span className="text-[10px] uppercase tracking-[0.2em]">Foco</span>
                                </button>
                                <button onClick={() => setActiveTab('simulation')} className={`w-full flex items-center gap-4 px-6 py-4 rounded-2xl transition-all duration-300 btn-hover ${activeTab === 'simulation' ? 'gold-bg text-black font-bold shadow-2xl scale-[1.02]' : 'card-dark text-slate-400 hover:bg-[#222]'}`}>
                                    <Icon name="rotate" size={18}/> <span className="text-[10px] uppercase tracking-[0.2em]">Ruleta</span>
                                </button>
                                
                                <div className="mt-12 p-5 rounded-2xl bg-red-950/10 border border-red-900/20">
                                    <div className="flex items-center gap-2 text-red-500 mb-3 font-bold text-[10px] uppercase tracking-widest">
                                        <Icon name="shield" size={14}/> Disciplina
                                    </div>
                                    <p className="text-[10px] leading-relaxed text-slate-500 italic font-light">Desvíos éticos o de caja generan sanción o despido inmediato.</p>
                                </div>
                            </nav>

                            <main className="lg:col-span-3 card-dark rounded-[2.5rem] p-8 md:p-12 shadow-2xl min-h-[600px] flex flex-col">
                                {activeTab === 'weekly' && (
                                    <div className="animate-in fade-in duration-700 flex-1">
                                        <h2 className="text-2xl font-light text-white mb-10 tracking-widest uppercase flex items-center gap-4">
                                            <span className="w-8 h-[1px] gold-bg"></span> Estándares Fijos
                                        </h2>
                                        <div className="grid gap-5">
                                            {[
                                                { t: "Presentación", d: "Presentarse ante el cliente al bajar la carta." },
                                                { t: "Uniforme", d: "Uniforme completo y presencia impecable." },
                                                { t: "Segundo Bocado", d: "Control de calidad a los 2 minutos de servido." },
                                                { t: "Limonadas", d: "Consultar: ¿Con o sin almíbar?" }
                                            ].map((item, i) => (
                                                <div key={i} className="bg-black/20 p-6 rounded-2xl border-l-4 gold-border shadow-inner">
                                                    <h3 className="gold-text font-bold text-[10px] uppercase tracking-[0.3em] mb-2">{item.t}</h3>
                                                    <p className="text-slate-400 text-sm italic font-light tracking-wide leading-relaxed">{item.d}</p>
                                                </div>
                                            ))}
                                        </div>
                                    </div>
                                )}

                                {activeTab === 'daily' && (
                                    <div className="space-y-8 animate-in fade-in duration-700 flex-1">
                                        <h2 className="text-2xl font-light text-white mb-10 tracking-widest uppercase flex items-center gap-4">
                                            <span className="w-8 h-[1px] bg-yellow-600"></span> Foco Operativo
                                        </h2>
                                        <div className="grid md:grid-cols-2 gap-5">
                                            <div className="bg-black/30 p-8 rounded-3xl border border-white/5">
                                                <h3 className="gold-text font-bold mb-6 flex items-center gap-3 text-[11px] uppercase tracking-widest">
                                                    <Icon name="alert" size={18}/> Lista 86
                                                </h3>
                                                <div className="h-28 flex items-center justify-center border border-dashed border-white/10 rounded-2xl bg-black/40 text-slate-600 text-[10px] uppercase tracking-[0.2em] italic font-semibold text-center px-4">Informar Oralmente</div>
                                            </div>
                                            <div className="bg-black/30 p-8 rounded-3xl border border-white/5">
                                                <h3 className="gold-text font-bold mb-6 flex items-center gap-3 text-[11px] uppercase tracking-widest">
                                                    <Icon name="rotate" size={18}/> Días Anteriores
                                                </h3>
                                                <div className="h-28 flex items-center justify-center border border-dashed border-white/10 rounded-2xl bg-black/40 text-slate-600 text-[10px] uppercase tracking-[0.2em] italic text-center px-6 leading-relaxed">Hechos Relevantes</div>
                                            </div>
                                        </div>
                                        <div className="bg-[#c5a059]/5 p-12 rounded-[2.5rem] border border-[#c5a059]/10 text-center relative overflow-hidden group">
                                            <div className="absolute -top-10 -right-10 opacity-5 group-hover:opacity-10 transition-opacity">
                                                <Icon name="coffee" size={240}/>
                                            </div>
                                            <h3 className="gold-text font-bold text-[11px] uppercase tracking-[0.5em] mb-4 opacity-80">Venta Sugerida</h3>
                                            <p className="text-4xl font-light text-white tracking-[0.2em]">GRAN TÉ IDEAL</p>
                                        </div>
                                    </div>
                                )}

                                {activeTab === 'simulation' && (
                                    <div className="flex flex-col items-center justify-center flex-1 text-center">
                                        {!selectedResult && !isSpinning && (
                                            <div className="animate-in fade-in duration-500 px-6">
                                                <div className="w-20 h-20 gold-bg rounded-full flex items-center justify-center mx-auto mb-10 shadow-[0_0_60px_rgba(197,160,89,0.25)]">
                                                    <Icon name="rotate" size={32} className="text-black"/>
                                                </div>
                                                <h2 className="text-3xl font-light text-white mb-4 tracking-wider uppercase">Ruleta Técnica</h2>
                                                <p className="text-slate-500 text-sm italic mb-12 font-light max-w-xs mx-auto">Sorteo de conocimientos sobre café, vinos y protocolo de servicio.</p>
                                                <button onClick={handleSpin} className="px-16 py-6 bg-transparent border gold-border gold-text rounded-full hover:gold-bg hover:text-black transition-all font-bold tracking-[0.3em] text-[10px] btn-hover">LANZAR RULETA</button>
                                            </div>
                                        )}

                                        {isSpinning && (
                                            <div className="flex flex-col items-center gap-10">
                                                <div className="w-16 h-16 border-[3px] gold-border border-t-transparent rounded-full animate-spin-custom"></div>
                                                <p className="gold-text uppercase tracking-[0.4em] text-[10px] font-bold animate-pulse">Sorteando Personal...</p>
                                            </div>
                                        )}

                                        {selectedResult && !isSpinning && (
                                            <div className="w-full max-w-lg animate-in zoom-in duration-300">
                                                <div className="mb-12">
                                                    <p className="text-slate-500 text-[10px] uppercase tracking-[0.3em] mb-4 italic font-light tracking-widest">Seleccionado:</p>
                                                    <h3 className="text-3xl font-bold text-white mb-2 tracking-tight">*{selectedResult.person.name}*</h3>
                                                    <p className="gold-text text-[10px] font-bold uppercase tracking-[0.2em] opacity-80 italic">{selectedResult.person.pos}</p>
                                                </div>
                                                <div className="bg-black/60 p-10 rounded-[2.5rem] border-l-[6px] gold-border mb-12 text-left shadow-2xl relative overflow-hidden">
                                                    <p className="text-slate-600 text-[9px] uppercase font-bold mb-4 tracking-widest flex items-center gap-2">Pregunta del Día:</p>
                                                    <p className="text-2xl text-white font-light italic leading-tight">"{selectedResult.question}"</p>
                                                </div>
                                                <div className="flex flex-col sm:flex-row gap-4">
                                                    <button onClick={handleNextPerson} className="flex-1 bg-[#252525] text-[#c5a059] py-5 rounded-2xl text-[10px] font-bold uppercase tracking-widest flex items-center justify-center gap-3 border border-white/5 hover:bg-[#333] transition-all btn-hover">
                                                        <Icon name="userPlus" size={18}/> Otro Empleado
                                                    </button>
                                                    <button onClick={handleSpin} className="flex-1 gold-bg text-black py-5 rounded-2xl text-[10px] font-bold uppercase tracking-widest shadow-xl hover:bg-[#d4b06a] btn-hover">
                                                        Girar Ruleta
                                                    </button>
                                                </div>
                                            </div>
                                        )}
                                    </div>
                                )}
                            </main>
                        </div>

                        <footer className="mt-20 pt-8 border-t border-white/5 flex flex-col md:flex-row justify-between items-center gap-6">
                            <p className="text-slate-700 text-[8px] uppercase tracking-[0.6em]">© 1912 — CONFITERÍA LA IDEAL — BUENOS AIRES</p>
                            <div className="flex items-center gap-3">
                                <div className="w-1.5 h-1.5 rounded-full gold-bg shadow-[0_0_15px_rgba(197,160,89,1)] animate-pulse"></div>
                                <span className="text-slate-600 text-[8px] uppercase tracking-[0.2em] font-semibold">Protocolo Operativo Activo</span>
                            </div>
                        </footer>
                    </div>
                </div>
            );
        };

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
