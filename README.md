# Material_Quiz_AEG_ClausesCompundComplex
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Module: Compound & Complex Sentences</title>
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Font Awesome -->
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    
    <!-- React & Babel -->
    <script src="https://unpkg.com/react@18/umd/react.production.min.js" crossorigin></script>
    <script src="https://unpkg.com/react-dom@18/umd/react-dom.production.min.js" crossorigin></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: { fontFamily: { sans: ['Inter', 'sans-serif'] } }
            }
        }
    </script>

    <style>
        body { background-color: #f8fafc; }
        .fade-in { animation: fadeIn 0.5s ease-out forwards; }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div id="root"></div>

    <script type="text/babel">
        const { useState } = React;

        const SLIDES = [
            { 
                type: 'intro', 
                title: 'Compound & Complex Sentences', 
                desc: 'Mastering sentence structures for advanced writing.' 
            },
            { 
                type: 'lesson', 
                topic: 'Compound Sentences', 
                theme: 'blue', 
                icon: 'fa-link',
                cards: [
                    { title: 'Definition', desc: 'Two independent clauses joined together.', icon: 'fa-equals' },
                    { title: 'Coordinating Conjunctions', desc: 'FANBOYS: For, And, Nor, But, Or, Yet, So.', icon: 'fa-handshake' },
                    { title: 'Example', desc: '"I wanted to go for a walk, but it started raining."', icon: 'fa-pen' }
                ]
            },
            { 
                type: 'lesson', 
                topic: 'Complex Sentences', 
                theme: 'emerald', 
                icon: 'fa-code-branch',
                cards: [
                    { title: 'Definition', desc: 'One independent clause and at least one dependent clause.', icon: 'fa-diagram-project' },
                    { title: 'Subordinating Conjunctions', desc: 'Because, Since, Although, When, While, If.', icon: 'fa-anchor' },
                    { title: 'Example', desc: '"Because it was raining, I stayed inside."', icon: 'fa-pen' }
                ]
            },
            { 
                type: 'quiz', 
                topic: 'Knowledge Check', 
                theme: 'orange',
                questions: [
                    { q: 'Which conjunction is used in a compound sentence?', options: ['Although', 'Because', 'But'], answer: 2 },
                    { q: 'Identify the sentence type: "While I was studying, the phone rang."', options: ['Simple', 'Compound', 'Complex'], answer: 2 }
                ]
            },
            { type: 'outro' }
        ];

        const getThemeStyles = (theme) => {
            switch(theme) {
                case 'blue': return 'text-blue-600 bg-blue-50 border-blue-200';
                case 'emerald': return 'text-emerald-600 bg-emerald-50 border-emerald-200';
                case 'orange': return 'text-orange-600 bg-orange-50 border-orange-200';
                default: return 'text-slate-600 bg-slate-50 border-slate-200';
            }
        };

        function App() {
            const [currentSlide, setCurrentSlide] = useState(0);
            const [score, setScore] = useState(0);

            const next = () => { if (currentSlide < SLIDES.length - 1) setCurrentSlide(prev => prev + 1); };
            const prev = () => { if (currentSlide > 0) setCurrentSlide(prev => prev - 1); };
            
            const slide = SLIDES[currentSlide];

            return (
                <div className="min-h-screen flex flex-col items-center justify-center p-6">
                    <div className="w-full max-w-4xl bg-slate-200 h-2 rounded-full mb-6">
                        <div className="h-full bg-slate-800 transition-all duration-300" style={{ width: `${(currentSlide / (SLIDES.length - 1)) * 100}%` }}></div>
                    </div>

                    <div className="w-full max-w-4xl bg-white shadow-xl rounded-xl flex flex-col min-h-[500px] overflow-hidden">
                        
                        {slide.type !== 'intro' && slide.type !== 'outro' && (
                            <header className={`px-6 py-4 border-b flex items-center space-x-3 ${getThemeStyles(slide.theme).split(' ')[1]}`}>
                                <i className={`fas ${slide.icon} text-xl ${getThemeStyles(slide.theme).split(' ')[0]}`}></i>
                                <h2 className={`font-bold text-lg ${getThemeStyles(slide.theme).split(' ')[0]}`}>{slide.topic}</h2>
                            </header>
                        )}

                        <main className="flex-grow p-8 flex flex-col justify-center fade-in" key={currentSlide}>
                            {slide.type === 'intro' && (
                                <div className="text-center">
                                    <h1 className="text-4xl font-bold text-slate-800 mb-4">{slide.title}</h1>
                                    <p className="text-lg text-slate-500">{slide.desc}</p>
                                </div>
                            )}

                            {slide.type === 'lesson' && (
                                <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
                                    {slide.cards.map((card, i) => (
                                        <div key={i} className="p-6 border rounded-lg shadow-sm hover:shadow-md transition-shadow bg-white">
                                            <i className={`fas ${card.icon} text-3xl mb-4 ${getThemeStyles(slide.theme).split(' ')[0]}`}></i>
                                            <h3 className="font-bold text-slate-800 mb-2">{card.title}</h3>
                                            <p className="text-slate-600 text-sm">{card.desc}</p>
                                        </div>
                                    ))}
                                </div>
                            )}

                            {slide.type === 'quiz' && (
                                <div className="space-y-6">
                                    {slide.questions.map((q, i) => (
                                        <div key={i} className="bg-slate-50 p-6 rounded-lg border">
                                            <p className="font-semibold text-slate-800 mb-4">{i + 1}. {q.q}</p>
                                            <div className="flex space-x-4">
                                                {q.options.map((opt, j) => (
                                                    <button key={j} onClick={() => { if(j === q.answer) setScore(score + 1) }} className="px-4 py-2 bg-white border rounded hover:bg-slate-100 transition-colors focus:ring-2 ring-orange-400">
                                                        {opt}
                                                    </button>
                                                ))}
                                            </div>
                                        </div>
                                    ))}
                                </div>
                            )}

                            {slide.type === 'outro' && (
                                <div className="text-center">
                                    <h2 className="text-3xl font-bold text-slate-800 mb-4">Module Complete!</h2>
                                    <p className="text-lg text-slate-600">Great job reviewing compound and complex sentences.</p>
                                </div>
                            )}
                        </main>

                        <footer className="px-6 py-4 bg-slate-50 border-t flex justify-between items-center">
                            <button onClick={prev} disabled={currentSlide === 0} className="px-4 py-2 font-semibold text-slate-600 disabled:opacity-50 hover:bg-slate-200 rounded">Back</button>
                            <span className="text-slate-400 font-bold">{currentSlide + 1} / {SLIDES.length}</span>
                            <button onClick={next} disabled={currentSlide === SLIDES.length - 1} className="px-4 py-2 font-semibold text-white bg-slate-800 disabled:opacity-50 hover:bg-slate-700 rounded">Next</button>
                        </footer>
                    </div>
                </div>
            );
        }

        const root = ReactDOM.createRoot(document.getElementById('root'));
        root.render(<App />);
    </script>
</body>
</html>
